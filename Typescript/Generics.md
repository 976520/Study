# 제네릭

Generics는 type을 담는 변수라고 생각하면 편하다. Type을 지정할 대상의 선언지점이 아니라 실질적인 객체의 생성지점에서 그 type을 지정할 수 있게 해준다. 따라서 같은 함수에서 다양한 type의 interface가 생성될 수 있다.

---

## 문법

`<Generic명>`을 함수명 뒤에 붙여서 사용한다. Generic명은 알파벳 대문자 1글자를 쓰는 것이 관례이다.

```tsx
function identity<T>(arg: T): T {
  return arg;
}
```

이 코드에서는 `<T>`가 generic type을 의미한다. 이 type은 함수의 매개변수와 반환값에 사용된다. 이러한 함수를 사용할 때는 다음과 같이 타입을 지정한다.

```tsx
const A = identity<number>(123);
const B = identity(123);
```

`A`는 `<number>`로써 generic type을 지정하였다. 이 경우, `identity` 함수의 `T`는 `number`로 대체된다. 하지만 `B`는 따로 type을 지정하지 않고 함수를 냅다 호출하였다. 이 경우 compiler가 알아서 type을 추론해준다.

만약 인수로 array를 넣어야 한다면,

```tsx
function identity<T>(arg: T[]): T[] {
  return arg;
}
```

이렇게 하거나,

```tsx
function identity<T>(arg: Array<T>): Array<T> {
  return arg;
}
```

이런식으로 명시해주어야 한다.

---
