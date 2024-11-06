## feature-sliced design

1. 이해

   <img src="https://github.com/user-attachments/assets/dddd769b-d1b2-48be-bd0b-c21ab7f7a0fa" width="600"/>

   FSD 디자인은 애플리케이션을 각각의 기능(feature)을 기준으로 분할하여 설계하는 방법이다.

   프로젝트를 처음 만들 때, directory를 걍 만들고,

   FSD에서는 `src` 디렉토리 아래에 있는 모든 폴더의 depth를 최대 3단계로 제한하며, 이는 layers, slices, segments의 세 level로 구성된다.

   1. layers

      모든 directory를 기능에 따라 layer로 분할하게 된다. Layers의 종류를 계층 순으로 나열하면 다음과 같다. 이때, layered architecture를 따르기 때문에 하위 계층에서 정의된 코드를 상위 계층에서 사용할 수 있으나, 반대의 경우는 불가능하다.

      1. `app`

         전체 application이 초기화되는 코드가 위치한다. providers, routers, global styles, global type declarations 등이 여기에 위치하게 된다.

      2. `pages`

         전체 page를 구성하기 위한 코드가 위치한다. `features`, `entities`, `widgets` 등의 layer에 포함된 코드들을 이용하여 각 page를 구성하게 된다.

         Page는 보통 router를 통해 관리되는 브라우저 주소 단위의 component들을 뜻한다.

      3. `widgets`

         각 page에서 재사용되는 독립적인 UI components들을 위치시킨다. `entities`, `features` 등의 layer에 포함된 코드들을 결합하여 각 widget을 구성하게 된다.

      4. `features`

         Business value를 제공하는 user sinario와 같은 기능이 위치한다.

      5. `entities`

         Business entity를 나타내는 코드가 위치한다.

      6. `shared`

         libs, API 등 특정 business logic에 속하지 않는 components들이 위치한다. UI kit, axios 설정, type 설정 등이 여기에 포함된다.

   2. slices

      각 layer 내에서 기능별로 다시 분할하게 된다. Slices의 이름은 정해져있지 않으며, 프로젝트 내에서 그 목적에 따라 설정된다.

      `app`과 `shared` layer는 slices를 가지지 않으며, 바로 segments로 이어진다.

   3. segments

      각 slice로 포함된 한 기능 내에서 가장 세부적인 구성 요소나 모듈을 나타낸다. 기능에 따라 필요한 코드가 다르겠지만, 보통 다음과 같은 코드들이 위치한다.

      1. api

      2. UI

      3. model

      4. lib

      5. config

      6. consts

---
