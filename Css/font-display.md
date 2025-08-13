## font-display

1.  이해
   
    글꼴을 로드하는 전략은 다음과 같은 두 종류가 있다.

      1. FOIT (Flash of Invisible Text)
    
          브라우저가 글꼴을 다운받을 때까지 글자를 보여주지 않는 것이다. 브라우저는 FOIT을 선호하여, `font-display`속성을 지정하지 않거나, `auto`로 하면 FOIT가 적용된다.
    
      2. FOUT (Flash of Unstyled Text)
   
          브라우저가 글꼴을 다운로드하기 전까지 글꼴이 적용되지 않은 Unstyled Text를 보여주는 것이다. 
    
    이러한 글꼴 렌더링을 조절하기 위한 것이 `font-display` 속성이다.


2.  속성

    1. auto

        기본값이다.

    3. swap

        <img width="734" height="240" alt="Image" src="https://github.com/user-attachments/assets/25d3eefd-35fc-4f6f-b20a-17aa37a111ea" />

        글꼴이 로드되기 전까지 계속 시스템 글꼴을 사용하다가 다운로드가 완료되면 적용한다.

    4. block

        <img width="734" height="344" alt="Image" src="https://github.com/user-attachments/assets/47d7dc10-c938-4900-9b61-2a546ea0a36c" />

        FOIT를 적용한다. 글꼴이 기간(3초) 내에 로드되지 않으면, 될 때 까지 시스템 글꼴을 사용하다가 교체한다.

    5. fallback

        <img width="734" height="445" alt="Image" src="https://github.com/user-attachments/assets/d131b674-2429-4b27-a97a-4f8743c45f0f" />

        `swap`과 비슷하지만 100ms만큼 block 속성을 가진다. 그 이후에 3초 내에 웹 글꼴이 로드되지 않는다면 계속 fallback 글꼴이 사용되는 것이다.

    6. optional

        <img width="1424" height="646" alt="Image" src="https://github.com/user-attachments/assets/7662ede1-0e01-499a-ba91-f1e987a12a05" />

        `fallback`과 비슷하지만 100ms안에 글꼴이 로드되지 않는다면, 그 후에는 글꼴이 로드되어도 교체하지 않는 속성이다.

---
