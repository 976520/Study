
## 렌더링

 [공식 문서](https://ko.react.dev/learn/render-and-commit)에서는 다음과 같이 정의한다.

> “렌더링”은 React에서 컴포넌트를 호출하는 것입니다.

'Component를 호출한다'는 **'React element를 return받는다'**와 같다. [모르겠으면 보고오자.](https://velog.io/@haensol/React-Element)

<img src="https://velog.velcdn.com/images/cold_mental/post/bafa343d-9bd9-4cd3-bda0-569d0bd7ac47/image.png" width="400px">

React에서 'Render'는 상술했듯 Component를 호출하는 것만을 의미하며, 흔히 생각하는 DOM rendering은 React에서는 commit으로 불리는 것을 알 수 있다. 이제 이 Render에서 Commit으로 가는 과정에서 무슨 일이 일어나는지 정리해보자.


1. 과정

      <img src="https://velog.velcdn.com/images/haensol/post/e4a786ae-8b14-4cab-bc81-d2f156d44833/image.png" width="800"/>

    이 그림은 Component의 life cycle을 표현한 것인데, 유명하긴 하지만 오래되서 class형 component 기준으로 작성되어있다. 이를 참고하여 Rendering 과정을 정리해보자.


   - **Component 호출**

      그림에서는 `constructor`와 `getDerivedStateFromProps` 호출로 설명하고 있지만, 함수형 component의 경우 그냥 호출하는 것과 같다. 이때 state나 메모이제이션 관련 Hook이 실행된다.
      
       DOM에는 아무 변화가 없고, VDOM을 기반으로 rendering 준비만 한다고 생각하면 된다. `createElement()`가 호출되기 전 시점이니 VDOM은 아직 구성되지 않는다.

   - **VDOM Reconciliation**

      `shouldComponentUpdate`가 true일 때 `render()`가 호출되고, 함수형 component의 경우 그 자체가 `render()` 역할을 한다. 
      
      이때 element 기반으로 VDOM을 생성하고 Reconciliation 작업이 수행된다.

      update 작업은 여러 개의 **unitOfWork**으로 쪼개져 처리된다. 각 unitOfWork은 컴포넌트 트리 내의 Fiber node 하나에 대응하며, Reconciler는 변경점이 생겼을 때 Work들을 Scheduler에 등록하여 우선순위에 따라 순차적으로 처리한다. 
      
      이 덕분에 긴 연산을 중단하거나 연기할 수 있는 interruptible rendering이 가능해진다.

   - **Commit phase**

      Renderer는 Reconciliation이 완료된 VDOM의 변경된 부분만 DOM에 반영한다(DOM mutation). 실제 DOM 조작이 일어나므로 브라우저가 일관성있게 paint를 수행할 수 있도록 **동기적(synchronous)**으로 실행된다. 

      여기서 `componentDidMount`, `componentDidUpdate`와 같은 side effect 관련 lifecycle method를 호출하는데 알 필요 없고, `useEffect`가 이 시점에 호출된다.

   그림에 따르면 여기서 **VDOM Reconcliation 까지가 Render Phase**로, 순수(pure)하며, DOM에 직접 영향을 주지 않고 side effect 없이 반복 가능하거나 중단될 수 있는 연산들로 구성된다. 
   
2. Rendering과 Reconciliation

    얼핏 비슷해 보일 수 있지만, [React는 rendering 환경과 Reconciliation 과정을 완전히 분리해 놓았다.](https://github.com/facebook/react/tree/v19.1.0/packages) 왜냐하면 Renderer는 렌더링 환경에 의존적이기 때문이다. 

    ![](https://velog.velcdn.com/images/haensol/post/10b2c9e5-1192-4bd6-9150-5129011c8682/image.png)

    실제 구조를 보면, 브라우저 환경에서는 `react-dom` 패키지가 사용되고, 모바일 환경에서는 `react-native-renderer` 패키지가 사용된다.

    **Reconciler는 무엇이 변경되었는지 계산하고, 이에 의존성을 가진 Renderer가 렌더링 환경과 react를 연결하여 변경 사항을 적용**하는 방식이다.


---