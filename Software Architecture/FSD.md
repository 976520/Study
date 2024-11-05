## feature-sliced design

1. 이해

   FSD 디자인은 애플리케이션을 각각의 기능(Feature)을 기준으로 분할하여 설계하는 방법이다.

   FSD에서는 `src` 디렉토리 아래에 있는 모든 폴더의 depth를 최대 3단계로 제한하며, 이는 layers, slices, segments의 세 계층으로 구성된다.

   1. layers

      모든 directory를 기능에 따라 layer로 분할하게 된다. Layers의 종류는 다음과 같다.

      1. `app`

      2. `pages`

      3. `widgets`

      4. `features`

      5. `entities`

      6. `shared`

   2. slices

      각 layer 내에서 기능별로 다시 분할하게 된다. Slices의 이름은 정해져있지 않으며, 프로젝트 내에서 그 목적에 따라 설정된다.

      `app`과 `shared` layer는 slices를 가지지 않으며, 바로 segments로 이어진다.

   3. segments

      각 slice로 포함된 한 기능 내에서 가장 세부적인 구성 요소나 모듈을 나타낸다.

---
