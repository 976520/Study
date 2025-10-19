# 이밴트 루프와 태스크 큐

JS는 한 번에 하나의 task만 실행할 수 있는 방식인 **single thread** 방식을 취한다. 그러나 이벤트 루프를 통해 비동기 작업을 처리하면서 마치 **multi thread**로 동작하는 척을 한다.

> JS의 concurrency(동시성)을 지원하는 것이 event loop이다.

<img width="600" alt="Image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/123460320/498167071-a37294eb-5e2e-4aa5-95e0-67117b394479.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20251007%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20251007T090147Z&X-Amz-Expires=300&X-Amz-Signature=2ba879c79f1f98881be0c3c238cf935ef96857e72f675fc136970b0cf04801fa&X-Amz-SignedHeaders=host" />

---

## JS 엔진의 역할

JS 엔진은 이 두 영역으로 구분된다.

<img width="500" alt="Image" src="https://felixgerschau.com/static/87b4e1eb66afc84d49da13af8e897367/5a190/garbage-collectoion-algorithm.png" />

- [Call stack](https://github.com/976520/Study/blob/main/Javascript/execution%20context.md#call-stack) 

    JS에서 함수가 실행될 때, 함수가 호출된 순서대로 call stack에 실행 컨텍스트가 push된다. JS 엔진은 **call stack이 단 하나** 있으며, 이는 '동시에' 2개 이상의 함수를 실행할 수 없다는 의미이다. call stack의 top을 제외한 모든 실행 컨텍스트는 모두 대기 중인 것이다.

- Heap = Memory Heap

     heap은 실제 객체가 저장되는 메모리 공간인데, call stack의 실행 컨텍스트가 heap 상의 객체를 참조한다. heap은 call stack과 달리 구조화되어있지 않다는 특징이 있는데, 객체는 크기가 고정되어 있지 않아서 정적으로 stack에 올릴 수 없기 때문에 **runtime에 동적으로 메모리를 할당할 수 있는 heap**에 저장되는 것이기 때문이다.

뭔가 복잡한게 있을 것 같지만, JS 엔진은 단순히 call stack을 통해 코드를 순차적으로 실행할 뿐이다. 비동기 처리와 같은 나머지 모든 작업은 JS 엔진을 구동하는 runtime 환경인 브라우저(또는 Node.js)가 한다.

---

## 브라우저의 역할

브라우저는 JS의 원활한 실행을 위해 다음을 제공한다.

브라우저는 JS 엔진과 별도의 공간이기 때문에 multi thread에서 처리된다. 이것이 

1. Task queue = Event queue = Callback queue

    > 비동기 작업을 잠시 등록해놓는 queue이다.

    <img width="500" alt="Image" src="https://velog.velcdn.com/images/onedanbee/post/2dcd1be1-f139-4f6a-8ba9-a32d2340da87/image.gif" />

    Task queue는 다음 두 종류로 나뉜다.

    - Microtask queue = Micro queue

    - Macro queue

2. Event loop

3. Web APIs

   > 브라우저의 기능들을 쉽게 이용할 수 있도록 도와주는 interface이다.

   - 하나 이상의 JS 객체를 이용하여 동작한다.
   
   - API의 일종이기 때문에 진입점(entry point)가 항상 존재한다.

   - 이벤트를 사용해 상태를 변경한다.

   - [하는 일이 많은 만큼 종류가 많다.](https://developer.mozilla.org/ko/docs/Web/API)