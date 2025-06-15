## **Virtual DOM**

만약 페이지의 특정 요소의 style을 변경하려고 한다면, **브라우저가 해당 요소를 찾아서 색상을 변경한 후 이를 화면에 반영하기 위해 해당 요소부터 그 하위 요소까지 모두 다시 그리게 된다.** 이러한 일련의 과정을 DOM구조나 레이아웃의 변경의 경우 Reflow, 요소의 외양적 변경의 경우 Repaint라고 칭한다. Reflow와 Repaint의 과정에서 많은 비용이 발생하는데, Virtual(가상의) DOM은 이를 완화하기 위해 등장했다.

**React는 렌더링이 발생할 때 마다 이러한 VDOM을 생성**한다. 이 VDOM은 우선 진짜 DOM의 가벼운 복사본 정도로 이해하면 되며, Element(plain object)로 존재한다.


1. Reconciliation 이해

      이는 [공식 문서](https://ko.legacy.reactjs.org/docs/reconciliation.html)에 다음과 같이 정의되어 있다.

      > Virtual DOM은 UI의 이상적인 또는 “가상”적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” DOM과 동기화하는 프로그래밍 개념입니다. 이 과정을 Reconciliation이라고 합니다.

      React 패키지 내부의 Reconciler가 이를 비교(diffing)하여 전체 app을 다시 rendering 하지 않고 실질적으로 **변경이 일어난 부분만 Renderer가 DOM에 update**한다. 이 비교 과정을 **Reconciliation**이라고 한다.

      Reconciliation 없이 전체 tree를 update하게 되면, 변경 사항의 규모와 관계없이 모든 node를 순회하고 비교해야 하므로 시간 복잡도가 $O(n^3)$에 가까워질 수 있다. 반면 React의 diffing 알고리즘은 여러 제약(key 기준 비교 등)을 두어 이를 대폭 줄이고, 대부분의 경우 선형 또는 준선형 수준으로 최적화한다. 실제 이 부분의 코드와 이슈를 보면 개발자들의 최적화를 위한 고군분투를 볼 수 있다...

2. Reconciliation 과정

    React는 항상 VDOM을 rendering 전, 후 버전으로 2개 가지고 있으며, 이는 총 2개의 tree로 구성된다. 이 tree들은 실제 element로 구성된 VDOM을 Fiber Node로 복사한 것이라고 이해하면 된다. 이렇게 똑같은 정보를 2번 가지고 있는 구조를 double buffering이라고 한다.

    <image src="https://goidle.github.io/static/258b43ce623e7b6340fc6aed969199ed/374ac/vDOM.png" width=500px/>

    - Root Node

      `createRoot()` 함수에 실제 DOM 요소를 props로 넘기면, Reconciler는 그 요소에 몇가지 플래그를 설정하고 `createFiberRoot()`를 호출하여 하나의 Fiber Root Node를 생성한다. 

      ```js
      // packages > react-reconciler > src > ReactFiberRoot.js

      export function createFiberRoot(
        ...
      ): FiberRoot  {
        ...
        // Cyclic construction. This cheats the type system right now because
        // stateNode is any.
        const uninitializedFiber = createHostRootFiber(tag, isStrictMode);
        root.current = uninitializedFiber;
        uninitializedFiber.stateNode = root;
        ...
      }
      ```  
      `createHostRootFiber()`로 생성된 Root Fiber Node인 `uninitializedFiber`는 초기 상태로 `root.current`에 연결되고, 해당 `uninitializedFiber`는 다시 자신이 속한 root를 stateNode로 참조한다. 주석에 나와있는 것처럼 순환 구조이다.

      이를 통해 후술할 두 개의 tree를 번갈아 관리하는 entry point 역할을 한다는 것을 유추할 수 있다.

    - current

      실제 DOM tree를 Fiber로 표현한 것이다. 다른 말로 지금 React 앱이 브라우저 상에 보여지고 있는 모습을 반영한 tree이다. 부모는 첫 번째 자식을 child로 참조하고, 자식은 부모를 return으로 참조한다. 한가지 특징은, 자식 node가 여러개일 때 나머지 자식들은 sibling으로 참조한다는 것이다.

    - workInProgress

      ```js
      // packages > react-reconciler > src > ReactFiber.js

      export function createWorkInProgress(current: Fiber, pendingProps: any): Fiber {

        let workInProgress = current.alternate;
        if (workInProgress === null) {
          workInProgress = createFiber(
            current.tag,
            pendingProps,
            current.key,
            current.mode,
          );
          workInProgress.elementType = current.elementType;
          workInProgress.type = current.type;
          workInProgress.stateNode = current.stateNode;

          workInProgress.alternate = current;
          current.alternate = workInProgress;
        }
      ...  

      }
      ```

      `current.alternate`가 null이면 `createFiber()`로 새 Fiber Node를 생성하고, 새 Fiber Node의 alternate를 current로 지정하고, current의 alternate를 새 Fiber Node로 지정하는 식으로 교차 참조되도록 한다. 이를 통해 workInProgress는 current tree를 복제하고 각 node가 alternate로 서로 참조하는 tree임을 알 수 있다. 
      
      **render phase에서 새로운 상태/props/render 결과를 반영하기 위해 이 tree를 조작한다.**

      ```jsx
      // packages > react-reconciler > src > ReactFiberWorkLoop.js

      function flushAfterMutationEffects(): void {
        ...

        // The work-in-progress tree is now the current tree. This must come after
        // the mutation phase, so that the previous tree is still current during
        // componentWillUnmount, but before the layout phase, so that the finished
        // work is current during componentDidMount/Update.
        root.current = finishedWork;
        pendingEffectsStatus = PENDING_LAYOUT_PHASE;
      }
      ```

      모든 작업이 끝나면 commit phase에서 기존에 Root Node가 새로운 workInProgress를 참조한다. 실제 주석에도 **'The work-in-progress tree is now the current tree.'** 라고 설명되어 있다. 이 시점이 잘못되면 lifecycle method에서 참조하는 tree가 엇갈리는 문제가 일어날 수 있기 때문에, 이것도 주석에 추가로 설명해놓은 모습이다.

3. 결론 

    Virtual DOM은 직접적인 DOM 조작 대신 메모리 상의 추상화 계층을 제공하며, Reconciliation은 이를 바탕으로 실제 DOM과 동기화한다. 이러한 구조는 렌더링 비용 최소화와 UX 향상에 목적을 둔다. 

---
