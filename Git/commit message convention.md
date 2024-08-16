# 저처럼 커밋 메시지 대충 쓰면 안됩니다

> Commit message convention은 commit을 할 때 commit message를 작성하는 규칙이다.

---

## 개념

변수명과 함수명의 naming convention은 camel case, snake case, pascal case 등이 있다. 이는 프로그램 상에서 강제된 것은 아니지만, 편의를 위해 개발자들끼리 약속한 것이다. commit message에도 이와 같은 convention이 있다.

개인 프로젝트를 혼자 개발할 때에는 commit message를 대충 작성하여도 무관하지만, 팀원과 함께 협업을 할 때에는 그럴 수 없다~~폐급~~. 모든 팀원이 이해할 수 있도록 commit message의 형식을 정하는 것이 commit message convention이다.

이 commit message convention은 여러 종류가 있고, 팀원끼리 정의하기 나름이지만 보통 udacity를 많이 사용하므로 본문에서는 udacity를 설명한다.

---

## 구조

공백을 기준으로 title, body, footer 영역을 나눈다.

```
type: Subject

body

footer
```

1. title

   Title 영역에는 type과 subject를 :(콜론)과 공백으로 구분하여 작성한다.

   Type이란 아래와 같이 대략적인 업데이트 작업의 종류를 나타낸다.

   |          |                                                                    |
   | -------- | ------------------------------------------------------------------ |
   | Feat     | 새로운 기능 추가                                                   |
   | Fix      | 버그 수정                                                          |
   | Docs     | 문서 수정                                                          |
   | Style    | 로직의 영향이 없는 formatting 등의 코드 변경                       |
   | Refactor | Refactoring                                                        |
   | Test     | 로직에 영향이 없는 text 코드 추가                                  |
   | Chore    | 코드의 변경이 없는 build 설정, package manager 변경 등의 기타 변경 |
   | Design   | UI 디자인 변경                                                     |
   | Comment  | 주석 업데이트                                                      |
   | Init     | 프로젝트 초기 생성                                                 |
   | Rename   | 파일명, 폴더명 수정 혹은 경로 변경                                 |
   | Remove   | 파일, 폴더 삭제                                                    |
   | Ci       | Ci 설정 파일 변경                                                  |
   | Perf     | 성능 향샹                                                          |

   Type 뒤에 이어지는 subject는 commit message의 제목이며, 변경사항을 개조식 구분으로 간결하게 작성한다. 따라서 50자 이내로 작성하여야 하며 마침표를 포함한 특수문자는 사용하지 않는다. 영문으로 작성할 경우 첫글자는 대문자를 쓰고 동사원형을 문장의 맨 앞에 배치하여 명령문 형태로 작성하며 과거시제는 사용하지 않는다.

2. body

   본문 영역으로, 업데이트 내역을, 그 중 무엇을, 왜 변경하였는지 상세히 설명한다. 생략할 수 있으며, 72자를 넘지 않도록 한다.

3. footer

   Issue 추적을 위한 영역이다. Issue tracker의 type과 issue 번호를 다음과 같은 형식으로 작성한다.

   ```
   [type]: #[issue number]
   ```

   이때 issue tracker type의 종류는 다음과 같다.

   |            |                                 |
   | ---------- | ------------------------------- |
   | Fixes      | 수정 중                         |
   | Resolves   | 해결됨                          |
   | Ref        | 참조할 issue 없음               |
   | Related to | 해당 commit에 관련된 issue 번호 |

---
