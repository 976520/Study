# Fiber

Fiber node는 rendering에 필요한 정보를 가진 object이자, Reconciliation 작업 단위이다.

Fiber Reconciler는 stack frame을 가상으로 memory에 저장해뒀다가, 필요한 시점에 돌아가 처리하도록 구현되어 있다. 

---

## 등장 배경

1. 브라우저의 JS 엔진이 single thread이기 때문에, 모든 JS 코드는 순차적으로 실행된다. 

2. 일반적인 모니터는 보통 $\frac{1}{60}$초, 약 16.6ms마다 화면을 갱신한다. (화면 주사율)

여기서 짐작이 되는 사람도 있을 것이다. Fiber Reconciler는 **작업을 unitOfWork으로 쪼개고 비동기로 치밀하게 scheduling하여 한 작업이 16.6ms 이상 thread를 점유하지 않게 하도록** 설계되어 있다. Fiber node 하나가 unitOfWork에 대응한다. 이를 통해 **작업을 일시중단하고 재시작**하거나, **수행 중인 작업보다 우선순위가 높은 작업이 인입될 경우 작업을 중단하고 인입된 작업 처리 후 재개**할 수 있게 되었다. 만약 Stack처럼 데이터를 꺼낼 수 있는 순서가 정해져 있다면, 이렇게 rendering의 순서를 유연하게 할 수 없다.

---

## Fiber Node 구조

VDOM이 DOM에 적용되기 때문에, **React element가 DOM에 반영되기 위해 먼저 VDOM에 추가되어야 한다.** React element 자체로 바로 VDOM에 추가할 수 없기 때문에, component의 state와 life cycle, hook등 데이터를 더해서 확장한 것이 Fiber이다. 

[실제 React에서 Fiber가 구현된 코드이다.](https://github.com/facebook/react/blob/v19.1.0/packages/react-reconciler/src/ReactFiber.js)

```jsx
function FiberNode(
  this: $FlowFixMe,
  tag: WorkTag,
  pendingProps: mixed,
  key: null | string,
  mode: TypeOfMode,
) {
  this.tag = tag;
  this.key = key;
  this.elementType = null;
  this.type = null;
  this.stateNode = null;

  this.return = null;
  this.child = null;
  this.sibling = null;
  this.index = 0;

  this.ref = null;
  this.refCleanup = null;

  this.pendingProps = pendingProps;
  this.memoizedProps = null;
  this.updateQueue = null;
  this.memoizedState = null;
  this.dependencies = null;

  this.mode = mode;

  this.flags = NoFlags;
  this.subtreeFlags = NoFlags;
  this.deletions = null;

  this.lanes = NoLanes;
  this.childLanes = NoLanes;

  this.alternate = null;

  if (enableProfilerTimer) {
    this.actualDuration = -0;
    this.actualStartTime = -1.1;
    this.selfBaseDuration = -0;
    this.treeBaseDuration = -0;
  }
}
```
