# 샤드시엔 유아이

> shadcn/ui는 radix-ui를 기반으로 하는 UI 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npx shadcn@latest init
```

## radix-ui

> radix-ui는 고품질의 엑세스 가능한 디자인 시스템 및 app을 구축하기 위한 UI component 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install radix-ui
```

radix-ui는 개발자들이 디자인 시스템을 쉽게 구축하도록 도와주는 Headless UI 라이브러리이다. 즉, UI나 UX보다는 DX를 위한 것이다. Headless UI 라이브러리는 디자인 없이 기능만 제공하는 component를 의미한다.

1. 디자인 시스템

   > 디자인 시스템은 디자인의 규격, 반복되는 component나 코드를 포함하는 UI 설계 규칙이다.

   디자인의 일관성을 위한 가이드라인이라고 이해하면 편하다. 이런 규칙이 있으면 한 프로덕트에서 어디는 빨강이고 어디는 파랑이고 그러면 정신없으니까 UIUX도 안좋아진다고 할 수 있다.

   자주 사용되는 UI 요소를 미리 정의해 놓으니까 개발자도 맨날 새로 구현할 필요 없고 편하다. 또한 디자이너나 다른 직군의 팀원들과도 동일한 가이드라인과 용어를 사용하기 때문에 의사소통 관점에서도 편리하다. 프로덕트를 확장할 때도 정의해놓은 가이드라인을 따르면 되니까 확장성도 좋다.

2. 사용

   말로만 하면 와닿지 않으니 바로 코드로 알아보자.

   ```tsx
   import { Button } from "@mui/material";
   import * as Popover from "@radix-ui/react-popover";

   const App = () => (
     <Popover.Root>
       <Popover.Trigger className="PopoverTrigger">
         <Button>누르면?</Button>
       </Popover.Trigger>
       <Popover.Portal>
         <Popover.Content className="PopoverContent">왜눌러</Popover.Content>
       </Popover.Portal>
     </Popover.Root>
   );
   ```

   이 코드에서는 `.Root`, `.Trigger`, `.Portal`, `.Content` component를 사용하였다. `.Root`는 최상위에 위치한 container이고, `.Trigger`는 Popover를 보여줄 event이고, `.Content`는 보여질
   콘텐츠이다. `.Portal`은 이 `.Content`가 DOM tree의 다른 위치에 렌더링되도록 하여 Popover가 다른 요소의 style에 영향을 받지 않도록 한다.

3. 특징

   1. Accessible

      '접근할 수 있는' 이라는 의미인데 한마디로 접근성 설정을 세세하게 할 수 있다는 뜻이다. Foucs 관련 설정이나 키보드 탐색? 뭐 그런걸 잘 할 수 있다.

   1. Unstyled

      라이브러리에서 component가 style 없이 제공되므로 개발자가 자유롭게 style을 조정할 수 있다.

## 개념

radix-ui에 style을 적용한 버전이 shadcn/ui 이다.
