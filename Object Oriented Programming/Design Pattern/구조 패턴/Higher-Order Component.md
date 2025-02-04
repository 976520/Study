## 고차 컴포넌트

1. 이해

   > Higher-Order Component는 다른 component를 인자로 받아 기능을 추가한 새 component를 반환하는 component이다.

   여러 component에서 동일한 logic을 사용하려 할 때 HOC(Higher-Order Component)를 사용하면 app 전체의 component 걸쳐 logic을 재사용할 수 있다.

2. 사용

   예를 들어 여러 component에 특정 style을 똑같이 적용하고 싶을 때, 매번 style 객체를 생성하는 대신

   ```tsx
   const Button: React.FC = () => <button style={{ color: "tomato" }}>asdf</button>;
   const Title: React.FC = () => <h1 style={{ color: "tomato" }}>asdf</h1>;
   ```

   component를 parameter로 받아 style 객체를 추가하여 반환하는 HOC를 만들 수 있다.

   ```tsx
   interface WithStyleProps {
     style?: React.CSSProperties;
   }

   function withStyle<P extends WithStyleProps>(Component: React.ComponentType<P>) {
     return (props: Omit<P, keyof WithStyleProps>) => {
       const style: React.CSSProperties = { color: "tomato" };
       return <Component style={style} {...(props as P)} />;
     };
   }

   const Button: React.FC = () => <button>asdf</button>;
   const Title: React.FC = () => <h1>asdf</h1>;

   const StyledButton = withStyle(Button);
   const StyledTitle = withStyle(Title);
   ```

   이 코드에서는 `withStyle`이라는 HOC를 만들어 `React.ComponentType<P>` type의 component를 parameter로 받아 style을 추가한 새로운 component를 반환하게끔 하였다.

   또한, **여러 HOC를 조합하여 사용**할 수 있다. 이전에 만든 `button`의 style을 마우스를 올렸을 때만 다르게 적용하는 기능을 추가하기 위해 `withHover`라는 HOC를 다음과 같이 만들어,

   ```tsx
   interface WithHoverProps {
     isHovered?: boolean;
     onMouseEnter?: () => void;
     onMouseLeave?: () => void;
   }

   function withHover<P extends WithHoverProps>(Component: React.ComponentType<P>) {
     return (props: Omit<P, keyof WithHoverProps>) => {
       const [isHovered, setIsHovered] = React.useState(false);

       const handleMouseEnter = () => setIsHovered(true);
       const handleMouseLeave = () => setIsHovered(false);

       return (
         <Component
           isHovered={isHovered}
           onMouseEnter={handleMouseEnter}
           onMouseLeave={handleMouseLeave}
           {...(props as P)}
         />
       );
     };
   }

   const HoverButton = withHover(withStyle(Button));
   const HoverTitle = withHover(withStyle(Title));
   ```

---
