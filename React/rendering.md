
## 렌더링

 [공식 문서](https://ko.react.dev/learn/render-and-commit)에서는 다음과 같이 정의한다.

> “렌더링”은 React에서 컴포넌트를 호출하는 것입니다.

'Component를 호출한다'는 **'React element를 return받는다'**와 같다. [모르겠으면 여기 보고오자.](https://velog.io/@haensol/React-Element)

1. 과정

    ![](https://velog.velcdn.com/images/haensol/post/e4a786ae-8b14-4cab-bc81-d2f156d44833/image.png)

    이 그림은 Component의 life cycle을 표현한 것인데, 이를 참고하여 Rendering 과정을 정리할 수 있다.

   - **Component 호출**
      `constructor`를 호출하고, `getDerivedStateFromProps` method를 실행하는 과정이다. DOM에는 아무 변화가 없다. 

   - **VDOM Reconcliation**
   `shouldComponentUpdate` -> `render`의 과정이다. 

   - **Mount**
      Renderer가 React element를 DOM에 삽입하는 과정(Commit Phase)이다. `componentDidMount`와 `componentDidUpdate`라는 side effect가 실행된다.

   - **Paint**
      브라우저가 DOM tree를 뿌리는 과정(Reflow/Repaint)이다. 이 부분은 React가 제어할 수 없다.

  그림에 따르면 여기서 **VDOM Reconcliation 까지가 Render Phase**로, 순수하고(pure) side effect가 없으며, 중단되거나 반복될 수 있다고 한다.

2. Rendering과 Reconcliation

    얼핏 비슷해 보일 수 있지만, [React는 rendering 환경과 Reconciliation 과정을 완전히 분리해 놓았다.](https://github.com/facebook/react/tree/v19.1.0/packages) 왜냐하면 Renderer는 렌더링 환경에 의존적이기 때문이다. 

    ![](https://velog.velcdn.com/images/haensol/post/10b2c9e5-1192-4bd6-9150-5129011c8682/image.png)

    실제 구조를 보면, 브라우저 환경에서는 `react-dom` 패키지가 사용되고, 모바일 환경에서는 `react-native-renderer` 패키지가 사용된다.

    **Reconciler는 무엇이 변경되었는지 계산하고, 이에 의존성을 가진 Renderer가 렌더링 환경과 react를 연결하여 변경 사항을 적용**하는 방식이다.
