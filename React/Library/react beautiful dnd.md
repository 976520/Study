## 디앤디

> 여기서 DND는 Drag and drop이라는 뜻으로, react beautiful dnd는 이걸 도와주는 라이브러리이다.

외부 라이브러리이기 때문에 별도로 설치가 필요하다.

```shell
npm install react-beautiful-dnd
```

참고로 Strictmode로 하면 라이브러리가 제대로 작동하지 않는다... 꼭 제거해주자.

---

1. `DragDropContext`

   > DND가 이루어지는 전체 영역이다.

   DND 로직을 작동시키기 위해서는 이 componunt를 가장 처음, 가장 상위에 정의해주어야 한다. 따라서 후술할 `Dropable`, `Dragable`이 지정된 영역을 모두 포함해야 하고, `onDragEnd`, `onDragStart` 함수를 바인딩한다.

2. `Dropable`

   > drop이 가능한 영역이다.

   `Dropable`은 Drop은 Drag가 끝나는 것이기 때문에, `onDragEnd`를 바인딩 받아 동작한다. DND에 대한 DOM을 그려주기 때문에 이에 따른 영역을 지정해줘야 한다.

3. `Dragable`

   > drag가 가능한 영역이다.

   `Dragable`은 Drag 동작이 시작될 수 있는 컴포넌트이다. 따라서 `onDragStart`를 바인딩 받아 동작한다.
