# 소프트웨어 아키텍쳐

> Software Architecture는 소프트웨어 구성요소들 사이에서 유기적 관계를 표현하고 소프트웨어의 설계와 업그레이드를 통제하는 원칙이다.

---

## 이해

Software Architecture는 system의 기본 구조이며, system을 구성하는 요소와 각 요소 간의 관계를 정의하는 설계도라고 할 수 있다. 이는 system의 주요 속성을 결정하고, 개발 과정의 주요 설계 과정을 통제하게 된다. 또한 system의 전반적인 templete를 제시하고, 이해관계자들 사이의 의사소통을 돕기도 한다.

Design Pattern과 비슷한 면이 많지만, Software Architecture는 보다 높은 수준의 추상화를 제시하며, 더 넓은 범위의 설계를 다룬다. 따라서 Software Architecture가 더 큰 범주에 속한다.

---

## 원칙

1.  modularity(모듈화)

2.  abstraction(추상화)

3.  encapsulation(캡슐화)

---

## Quality Attribute

> Quality Attribute(품질 특성)은 양이나 질로 관찰하여 측정할 수 있는 system의 속성이다.

1. implementation attributes

   Implementation attributes는 시스템의 구현 방법에 대한 속성이다. 즉, runtime시 관측되지 않는 구현 특성에서의 quality attributes이다.

   1. portability(이식성)

   2. interoperability(상호운용성)

   3. testability(테스트 용이성)

   4. maintainability(유지보수성), extensibility(확장성)

   5. scalability(확장성)

   6. flexibility(유연성)

2. runtime attributes

   Runtime attributes는 시스템의 실행 중 관찰 가능한 quality attributes이다.

   1. availability(가용성)

      Software가 필요할 때 작업을 수행할 준비가 되었는지 판단하는 척도이다. 오류 발생 시 system의 반응을 판단하여 오류를 완화시켜 서비스 중단 시간을 최소화하는 것이다.

   2. performance(성능)

      Event에 정해진 시간 내에 응답하여야 한다.

   3. security(보안성)

      인증되지 않은 access를 차단하고, 중요한 data를 보호하는 것이다. 비밀성 및 무결성을 보장한다.

   4. modifiability(변경용이성)

      - 변경 사항의 지역화

      - 파급효과의 방지

      - binding 시점의 연기

   5. testability(시험 용이성)

      Testing을 통해 오류를 찾아내고, 오류를 완화시키는 것이다.

   6. usability(사용성)

      사용자가 얼마나 쉽게 시스템을 사용할 수 있는지 측정하는 척도이다. 이를 통해 시스템의 기능을 쉽게 배워 사용할 수 있도록, 오류의 영향을 최소화하고, 사용자의 요구에 맞춰 시스템이 효율적으로 작동하도록 한다.

3. business attributes

   1. time to market(시장 적시성)

   2. cost and benefit(비용 및 효익)

   3. projected lifetime of the system(시스템의 프로젝트 생명 주기)

   4. targeted market(목표 시장)

   5. rollout schedule(발매 일정)

      현 제품이 기본적인 기능만을 제공하며, 차후에 추가적인 기능이 release될 예정이라면 architecture의 flexibility(유연성)와 customizability(특화성)가 중요한 품질속성이 된다. 출시 일정에 따라 제품의 특성이 달라질 수 있기 때문이다.

   6. integration with legacy systems(기존 시스템과의 통합)

      제공하려는 system이 기존 system과 통합되어야 할 경우, 적절한 통합 mechanism이 정의되어야 한다.

4. typical quality attributes trade-off pairs

---
