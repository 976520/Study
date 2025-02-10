# 제네릭

Generics는 type을 담는 변수라고 생각하면 편하다. Type을 지정할 대상의 선언지점이 아니라 실질적인 객체의 생성지점에서 그 type을 지정할 수 있게 해준다. 따라서 같은 함수에서 다양한 type의 interface가 생성될 수 있다.

일반적인 프로그래밍 언어의 변수처럼 TS에서 정말정말정말정말정말 많이 사용하는 문법이다.

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

## Generic 제약

말 그대로 Generic에 조건을 걸어 제약을 둘 수 있다.

1. type 제약

   다음은 `extends`를 사용하여 parameter의 type을 number로 제한한 예시이다.

   ```tsx
   function identity<T extends number>(arg: T): T {
     return arg;
   }
   ```

   만약 이 함수를 호출할 때 number가 아닌 다른 타입을 넣으면 에러가 발생한다.

   여러 type을 제한할 때는 &(앰퍼샌드)를 사용하거나,

   ```tsx
   function identity<T extends number & string>(arg: T): T {
     return arg;
   }
   ```

   이렇게 type을 따로 선언하여 사용할 수 있다.

   ```tsx
   type NumberOrString = number | string;

   function identity<T extends NumberOrString>(arg: T): T {
     return arg;
   }
   ```

2. 속성 제약

   특정 속성을 가진 객체만 받도록 제약할 수도 있다. 다음은 length 속성을 가진 객체만 받는 예시이다.

   ```tsx
   interface Lengthwise {
     length: number;
   }

   function IfYouWantToGetLength<T extends Lengthwise>(arg: T): number {
     return arg.length;
   }
   ```

   `interface`를 통해 length 속성을 가진 객체를 `Lengthwise`라는 이름으로 정의하였다. Generic에 `extends`를 통해 `Lengthwise`만 받을 수 있도록 제약을 두었기 때문에 결과적으로,

   ```tsx
   IfYouWantToGetLength("die");
   IfYouWantToGetLength([4, 6, 8]);
   ```

   string과 array는 모두 length 속성을 가지고 있기 때문에 위 코드는 모두 정상적으로 실행된다.

   ```tsx
   IfYouWantToGetLength(123);
   IfYouWantToGetLength<string>(123);
   ```

   하지만 number는 length 속성을 가지고 있지 않기 때문에 에러가 발생한다. 이걸 해결하겠답시고 어거지로 string으로 지정해봤자, 인수의 type과 generic type이 다르기 때문에 에러가 발생한다.

   또한 custom property를 가진 객체에 대해서도 제약을 걸 수 있다.

   ```tsx
   interface HasName {
     name: string;
     age: number;
   }

   function getNameAndAge<T extends HasName>(obj: T): string {
     return `${obj.name}은 ${obj.age}살입니다.`;
   }
   ```

   이렇게 정의된 함수에는 `name`과 `age` 속성을 가진 객체만 인수로 전달될 수 있다.

   ```tsx
   const person = { name: "이주언", age: 17 };
   console.log(getNameAndAge(person)); // 출력: 이주언은 17살입니다.
   ```

   그러나 다음과 같이 속성을 이상하게 전달하면 가차없이 에러가 발생한다.

   ```tsx
   const person = { name: "이주언", major: "flutter" };
   console.log(getNameAndAge(person));
   ```

---

## Generic Function

TypeScript에서는 함수 자체도 하나의 type이기 때문에 다음과 같이 interface로 정의할 수 있고,

```tsx
interface Add {
  (a: number, b: number): number;
}

const add: Add = (a, b) => {
  return a + b;
};
```

여기서 Generic을 사용할 수도 있다.

```tsx
interface Calculate<T> {
  (a: T, b: T): T;
}

const NumberCalculate: Calculate<number> = (a, b) => {
  return a + b;
};

const StringCalculate: Calculate<string> = (a, b) => {
  return a + b;
};

console.log(NumberCalculate(2, 8)); // 출력: 10
console.log(StringCalculate("White", "Ferrari")); // 출력: WhiteFerrari
```

이 코드에서는 `Calculate` interface를 구현한 `NumberCalculate`와 `StringCalculate` 함수를 정의하였다. 함수 호출 시 type이 각각 number와 string으로 추론되어 compile된다.

---

## Generic Class

만약 class에서 generic을 사용하면, 그 type은 해당 class의 모든 메서드에서 사용할 수 있다.

```tsx
class Container<T> {
  constructor(private item: T) {}

  getItem(): T {
    return this.item;
  }
}

const numberContainer = new Container<number>(123);
console.log(numberContainer.getItem()); // 출력: 123

const stringContainer = new Container<string>("see");
console.log(stringContainer.getItem()); // 출력: see
```

이 코드에서는 `Container` class를 generic class로 만들기 위해 class 이름 뒤에 `<T>`를 붙여 type parameter를 지정하였다. 이러면 **객체를 생성할 때** constructor에 전달하는 값의 type에 따라 자동으로 `T`의 type이 결정된다.

이렇게 한번 지정된 type `T`는 class 내의 모든 곳(constructor, method, 속성 등)에서 일관되게 사용된다.
이 코드에서 `getItem()` method는 constructor에서 받은 것과 동일한 type의 값을 반환하게 된다.

---
