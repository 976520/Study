# React Element

[공식 블로그](https://ko.legacy.reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html)는 Element를 다음과 같이 설명한다.

> An element is a plain object describing a component instance or DOM node and its desired properties.

## 예시

JSX로 함수형 component를 작성할 때 return 안에 HTML 비슷하게 생긴 걸 넣는다. 알다시피 Component는 props를 받아서 element를 return하는 것이다.

```jsx
function Counter() {
   const [count, setCount] = useState(0);

   return (
   <div>
      <p>Count: {count}</p>
      <Button onClick={() => setCount(count + 1)}>Click</Button>
   </div>
   );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Counter />);
```
이 심플한 코드를 통해 다음과 같은 사실을 알 수 있다.

- React element는 native DOM에 rendering할 수 없고 root를 통해 rendering해야 한다.

- 이 JSX 표현식을 JS 엔진이 이해할 수 있는 형태로 변환해야 한다.

   ```js
   return React.createElement(
         "div",
         null,
         React.createElement("p", null, `Count: ${count}`),
         React.createElement(Button, { onClick: () => setCount(count + 1) }, "Click")
   ); 
   ```
   
   이는 예시 코드의 return 부분을 Babel이 트랜스파일한 것이다. `createElement`에 props로 뭘 내려주고 있는데, 이것이 DOM node를 설명하기 위한 것임을 유추할 수 있다. 이제 `createElement`에서 return받는 JS object는 다음과 같다.
   
   ```js
   {
   $$typeof: Symbol.for('react.element'),
   type: 'div',
   key: null,
   ref: null,
   props: {
      children: [
         {
         $$typeof: Symbol.for('react.element'),
         type: 'p',
         key: null,
         ref: null,
         props: {
            children: `Count: ${count}`
         },
         _owner: null, 
         },
         {
         $$typeof: Symbol.for('react.element'),
         type: Button,
         key: null,
         ref: null,
         props: {
            onClick: () => setCount(count + 1),
            children: "Click"
         },
         _owner: null,
         }
      ]
   },
   _owner: null
   }
   ```  
   이제 Element가 다른 Element를 children으로 가질 수 있는 JS object라는 것을 이해했다. 
   
## 이해

[createElement를 통해 반환되는 ReactElement를 정의한 코드](https://github.com/facebook/react/blob/v19.1.0/packages/react/src/jsx/ReactJSXElement.js)이다. `createElement`의 경우 이 `ReactElement()`를 통해 JS 객체를 만드는 factory 함수 역할을 한다.

```js
function ReactElement(type, key, props) {
  const refProp = props.ref;
  const ref = refProp !== undefined ? refProp : null;
  let element;

  element = {
    $$typeof: REACT_ELEMENT_TYPE,
    type,
    key,
    ref,
    props,
  };

  return element;
}
```

하나씩 확인해보자.

- `$$typeof`

   이게 `Symbol.for('react.element')`이기 때문에 React 패키지 내에서 React Element를 식별할 수 있다. 사용자가 건들 수는 없다. 

- `type`

   어떤 HTML 태그, 혹은 Component인 지 나타낸다. 예시에서 `'p'`, `'div'`와 같은 HTML 태그도 들어가고, `Button`같은 Component도 들어가는 것을 확인할 수 있다. 이에 따라 DOM element와 Component element으로 구분되지만, 큰 차이는 없다.
    **왜냐하면 기존의 DOM node와 React component를 완전히 동일하게 쓸 수 있는 것이 element의 특징이자 도입 이유이기 때문이다.**

   > An element describing a component is also an element, just like an element describing the DOM node. They can be nested and mixed with each other.

- `key`, `ref`

   config 객체 안에 있는 것들인데, 각각 list 렌더링 최적화와 실제 DOM 또는 컴포넌트 인스턴스 참조를 위해 필요하다.

- `props`

   props 정보가 들어있다.

Component끼리 decoupled된다는 장점이 있다.

> This mix and matching helps keep components decoupled from each other, as they can express both is-a and has-a relationships exclusively through composition.

예시에서는 DOM element인 `div`가 그 children인 Component element `Button`이 has-a 관계이지만, 부모가 `Button`의 내부 Element tree에 접근할 수 없게끔 캡슐화되어있다. 따라서 return받는 element의 type이 모두 DOM element일 때 까지 `ReactElement()`를 재귀적으로 호출하며, 이 과정을 Top-down reconciliation이라고 한다.



## 결론

> The returned element tree can contain both elements describing DOM nodes, and elements describing other components. This lets you compose independent parts of UI without relying on their internal DOM structure.

update가 일어날 때 우리가 작성한 JSX를 element로 변환하는데 이 JS object가 우리가 아는 [VDOM](https://github.com/976520/Study/blob/main/React/virtual%20dom.mdx)을 이루게 된다. 

---