## **Virtual DOM**

만약 페이지의 특정 요소의 style을 변경하려고 한다면, **브라우저가 해당 요소를 찾아서 색상을 변경한 후 그를 적용하기 위해 해당 요소부터 그 하위 요소까지 모두 다시 그리게 된다.** 이러한 일련의 과정을 DOM구조나 레이아웃의 변경의 경우 Reflow, 요소의 외양적 변경의 경우 Repaint라고 칭한다. Reflow와 Repaint의 과정에서 많은 비용이 발생하는데, Virtual(가상의) DOM은 이를 완화하기 위해 등장했다.

**React는 렌더링이 발생할 때 마다 이러한 VDOM을 생성**한다. 이 VDOM은 우선 진짜 DOM의 가벼운 복사본 정도로 이해하면 되며, JS plain object 형태로 존재한다.

1. double buffering

    React는 항상 VDOM을 rendering 전, 후 버전으로 2개 가지고 있으며, 이는 총 2개의 tree로 구성된다.

    <image src="https://goidle.github.io/static/258b43ce623e7b6340fc6aed969199ed/374ac/vDOM.png" width=500px/>

    - Root Node

      `createRoot()` 함수에 실제 DOM 요소를 props로 넘기면, React는 그 요소를 기준으로 하나의 Fiber Root Node를 생성한다. 이는 후술할 두 개의 tree를 번갈아 관리하는 entry point 역할을 한다.

    - current

      실제 DOM tree를 Fiber로 표현한 것이다. 다른 말로 지금 React 앱이 브라우저 상에 보여지고 있는 모습을 반영한 tree이다.

    - workInProgress

      [실제 구현](https://github.com/facebook/react/blob/main/packages/react-reconciler/src/ReactFiber.js)을 보면, 

      ```js
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

      `current.alternate`가 null이면 `createFiber()`로 새 Fiber를 생성하고, 새 Fiber의 alternate를 current로 지정하고, current의 alternate를 새 Fiber로 지정하는 식으로 교차 참조되도록 한다. 이를 통해 workInProgress는 current tree를 복제하고 각 node가 alternate로 서로 참조하는 tree임을 알 수 있다. 
      
      render phase에서 새로운 상태/props/render 결과를 반영하기 위해 이 tree를 조작한다. 작업이 끝나면 commit phase에서 다시 current가 된다.

2. Reconciliation

    이는 [공식 문서](https://ko.legacy.reactjs.org/docs/reconciliation.html)에 다음과 같이 정의되어 있다.

    > Virtual DOM은 UI의 이상적인 또는 “가상”적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” DOM과 동기화하는 프로그래밍 개념입니다. 이 과정을 Reconciliation이라고 합니다.

   React 패키지 내부의 Reconciler가 이를 비교(diffing)하여 전체 app을 다시 rendering 하지 않고 실질적으로 **변경이 일어난 부분만 renderer를 통해 DOM에 update**한다. 이 과정을 **Reconciliation**이라고 한다.

Virtual DOM은 실제 DOM을 직접 조작하는 대신 간접적으로 조작하면서 비용을 절약하는 데에 목적을 둔다.

---
