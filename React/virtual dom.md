## **Virtual DOM**

만약 페이지의 특정 요소의 style을 변경하려고 한다면, **브라우저가 해당 요소를 찾아서 색상을 변경한 후 그를 적용하기 위해 해당 요소부터 그 하위 요소까지 모두 다시 그리게 된다.** 이러한 일련의 과정을 DOM구조나 레이아웃의 변경의 경우 Reflow, 요소의 외양적 변경의 경우 Repaint라고 칭한다. Reflow와 Repaint의 과정에서 많은 비용이 발생하는데, Virtual(가상의) DOM은 이를 완화하기 위해 등장했다.

이는 [공식 문서](https://ko.legacy.reactjs.org/docs/reconciliation.html)에 다음과 같이 정의되어 있다.

> Virtual DOM은 UI의 이상적인 또는 “가상”적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” DOM과 동기화하는 프로그래밍 개념입니다. 이 과정을 Reconciliation이라고 합니다.

**React는 렌더링이 발생할 때 마다 이러한 VDOM을 생성**한다. 이 VDOM은 우선 진짜 DOM의 가벼운 복사본 정도로 이해하면 되며, JS plain object 형태로 존재한다. 또한 React는 항상 VDOM을 렌더링 전, 후 버전으로 2개 가지고 있으며, React 패키지 내부의 Reconciler가 이를 비교(diffing)하여 전체 app을 다시 rendering 하지 않고 실질적으로 **변경이 일어난 부분만 DOM에 update**한다. 이 과정을 Reconciliation이라고 한다.

Virtual DOM은 실제 DOM을 직접 조작하는 대신 간접적으로 조작하면서 렌더링 성능을 향상시키는 데에 목적을 둔다.

---
