# AI-DECLARATION.md

[![AI-DECLARATION: copilot](https://img.shields.io/badge/䷼%20AI--DECLARATION-copilot-fee2e2?labelColor=fee2e2)](https://ai-declaration.md)

## 개요

AI를 활용한 코드 작성은 이제 거스를 수 없는 현실이 되었으며, 이는 우리에게 큰 편리함을 주기도 하지만 동시에 새로운 고민거리를 안겨주기도 합니다. 여기서 중요한 것은 코드 자체가 아니라 투명성과 명확성입니다. 적어도 이 명세는 이러한 전제를 바탕으로 합니다. 우리가 제안하는 바는 아주 단순합니다. 프로젝트 저장소에 으레 다른 파일들을 포함하듯이 구조화된 `AI-DECLARATION.md` 파일도 함께 추가하자는 것입니다. 이를 통해 AI를 어떻게 사용했는지 명명백백하게 밝히고, 더 나아가 이러한 실천을 개발 생태계의 보편적인 문화로 정착시키고자 합니다.

이는 향후 LLM이나 기타 코드 생성 도구의 사용을 막으려는 것이 아닙니다. 오히려 그 반대로, 이를 올바르게 활용할 수 있도록 돕는 장치입니다. 코드의 어느 부분이 AI로 작성되었는지 투명하게 밝히면, AI 코드에 의구심을 갖는 사람이라도 해당 부분만 집중적으로 살펴보고 교차 검증할 수 있습니다. 또한, 코드 작성자 입장에서는 자신의 순수 코딩 역량뿐만 아니라 프로젝트 기획력 등 다양한 소프트 스킬을 더욱 선명하게 입증할 수 있습니다.

### 명세

`AI-DECLARATION.md` 파일은 구조화된 데이터를 정의하기 위해 YAML 프런트매터를 사용하며, 그 아래 마크다운 본문에는 사람이 직접 읽고 맥락을 이해할 수 있도록 `## Notes`(참고 사항) 섹션을 반드시 포함해야 합니다. 최소한 `version` (버전), `level` (단계) 프런트매터 필드와 `## Notes` 섹션이 있어야 합니다.

필요하다면 개발 `processes`(과정)별 개별 단계를 명시할 수 있습니다. 이 때, 전역 `level`은 명시된 단계 중 가장 높은 단계로 지정되어야 합니다. 목록에 명시되지 않은 과정은 암묵적으로 `none`으로 간주됩니다. 또한 특정 `components`(파일 경로 또는 디렉터리)별로 단계를 명시하는 것도 가능합니다.

이 명세는 `version`, `level`, `processes`, `components`를 공식 규격으로 정의합니다.

#### 단계 (`level`)

- `none`: 어떠한 시점에서도 AI 도구를 사용하지 않음.
- `hint`: AI 자동 완성 또는 인라인 추천만 사용. 사람이 모든 코드를 작성하며, AI는 이따금 코드의 한 줄이나 블록을 완성함.
- `assist`: 사람이 주도함. 특정 작업(함수 구현, 코드 동작 설명, 테스트 초안 작성 등)에 대해 필요할 때 마다 AI가 사용되지만, AI가 전반적인 작업을 이끌지는 않음.
- `pair`: 작업 전반에 걸쳐 사람과 AI가 적극적으로 협업함. 기여도는 대략 비슷함.
- `copilot`: 사람이 기획하고 검토하는 동안 AI가 코드를 구현함. 사람이 완성할 결과물을 정의하고 검증하지만, 코드 작성의 대부분은 AI가 수행함.
- `auto`: 최소한의 지시만으로 AI가 자율적으로 작동함. 사람이 큰 틀에서 방향을 잡거나 결과물을 승인할 수는 있지만, 코드를 직접 작성하거나 세밀하게 지시하지는 않음.

#### 과정 (`processes`)

- `design`: 아키텍처, 시스템 설계 및 의사결정.
- `implementation`: 프로덕션 코드 작성.
- `testing`: 테스트 코드 작성, 테스트 계획 수립 및 품질 보증(QA).
- `documentation`: 문서, 주석, README 및 변경 로그 작성.
- `review`: 코드 리뷰 및 풀 리퀘스트(PR) 피드백.
- `deployment`: CI/CD 구성, 인프라 및 릴리스 스크립트 작성.

### 스키마

아래의 YAML 스키마는 `AI-DECLARATION.md` 파일의 구조를 형식적으로 규정합니다. 선언 파일을 검증하거나 관련 도구를 개발할 때 이 스키마를 사용하세요.

```yaml
type: object
required: [version, level]
definitions:
  level:
    type: string
    enum: [none, hint, assist, pair, copilot, auto]
properties:
  version:
    type: string
    pattern: "^[0-9]+\\.[0-9]+\\.[0-9]+$"
  level:
    $ref: "#/definitions/level"
  processes:
    type: object
    propertyNames:
      enum: [design, implementation, testing, documentation, review, deployment]
    additionalProperties:
      $ref: "#/definitions/level"
  components:
    type: object
    additionalProperties:
      $ref: "#/definitions/level"
additionalProperties: false
```

### 예시

아래에서 다양한 상황에 따른 예시를 확인할 수 있습니다.

#### 기본

가장 단순한 형태의 `AI-DECLARATION.md`에는 `version`, `level`, 그리고 `## Notes` 섹션이 있어야 합니다.

> 여기까지 리뷰 및 수정 완료.
>
> 이하는 초벌 번역 (기계번역)


```markdown
---
version: "0.1.1"
level: none
---

이 형식은 [AI-DECLARATION.md](https://ai-declaration.md/en/0.1.1)를 기반으로 합니다.

## Notes

- 어떠한 AI 도구도 사용하지 않았습니다.
```

```markdown
---
version: "0.1.1"
level: auto
---

이 형식은 [AI-DECLARATION.md](https://ai-declaration.md/en/0.1.1)를 기반으로 합니다.

## Notes

- 전체 애플리케이션을 제작하는 데 Claude Code를 사용했습니다.
```

#### `processes` 사용

개발 단계별 AI 참여도를 세밀하게 선언하려면 `processes`를 사용하세요. 전역 `level`은 명시된 단계 중 가장 높은 단계를 지정해야 합니다. 목록에 없는 과정은 암묵적으로 `none`으로 간주됩니다.

```markdown
---
version: "0.1.1"
level: auto
processes:
  design: auto
  testing: copilot
---

이 형식은 [AI-DECLARATION.md](https://ai-declaration.md/en/0.1.1)를 기반으로 합니다.

## Notes

- AI가 아키텍처 결정과 테스트 코드 생성을 주도했습니다. 모든 결과물은 사람이 검토했습니다.
```

#### `components` 사용

특정 파일이나 디렉터리의 AI 참여도를 선언하려면 `components`를 사용하세요.

```markdown
---
version: "0.1.1"
level: auto
components:
  src/helpers: auto
---

이 형식은 [AI-DECLARATION.md](https://ai-declaration.md/en/0.1.1)를 기반으로 합니다.

## Notes

- helpers 디렉터리는 100% AI가 생성했습니다. 그 외의 모든 코드는 사람이 직접 작성했습니다.
```

## 배지 (Badges)

`README` 파일에 배지를 추가하여 귀하의 `AI-DECLARATION` 단계를 한눈에 보여줄 수 있습니다. 단, 배지는 편의를 위한 것이며 명세서를 제대로 준수하려면 _반드시_ `AI-DECLARATION.md` 파일을 포함해야 합니다.

- [![AI-DECLARATION: none](https://img.shields.io/badge/䷼%20AI--DECLARATION-none-dcfce7?labelColor=dcfce7)](https://ai-declaration.md)
- [![AI-DECLARATION: hint](https://img.shields.io/badge/䷼%20AI--DECLARATION-hint-ecfccb?labelColor=ecfccb)](https://ai-declaration.md)
- [![AI-DECLARATION: assist](https://img.shields.io/badge/䷼%20AI--DECLARATION-assist-fef9c3?labelColor=fef9c3)](https://ai-declaration.md)
- [![AI-DECLARATION: pair](https://img.shields.io/badge/䷼%20AI--DECLARATION-pair-ffedd5?labelColor=ffedd5)](https://ai-declaration.md)
- [![AI-DECLARATION: copilot](https://img.shields.io/badge/䷼%20AI--DECLARATION-copilot-fee2e2?labelColor=fee2e2)](https://ai-declaration.md)
- [![AI-DECLARATION: auto](https://img.shields.io/badge/䷼%20AI--DECLARATION-auto-ede9fe?labelColor=ede9fe)](https://ai-declaration.md)

## 자주 묻는 질문 (FAQ)

### 선언 파일에 거짓말을 적으면 어떻게 되나요?
글쎄요, 그러면 이 선언의 목적 자체가 무의미해지겠죠? 이 아이디어의 핵심은 우리 모두가 신뢰할 수 있는 일종의 사회적 계약(social contract)을 맺는 데 있습니다. 저장소에 `AI-DECLARATION.md`가 보인다면, 누구나 이를 굳게 믿을 수 있는 단일 진실 공급원(single source of truth)으로 보자는 것입니다.

### 이 파일을 자동으로 생성하는 도구를 만들어도 되나요?
얼마든지 환영합니다. 저는 자동 생성 도구는 물론, 파싱(parsing) 도구 생태계가 마련되는 것을 기대하고 있습니다. 언젠가는 저도 직접 만들겠지만, 여러분의 모든 기여는 언제나 감사합니다.

### 번역에 기여해도 되나요?
물론입니다! 꼭 부탁드립니다. 저장소를 포크(fork)한 뒤 `README_ko.md`처럼 `README_<언어코드>.md` 파일을 추가해 주세요. 그런 다음 PR(Pull Request)을 올려주시면, 확인 후 처리하겠습니다.

### 명세 내용 변경을 제안하고 싶습니다.
이 프로젝트가 오픈소스라서 다행이네요! 이 명세서는 피드백과 PR을 통해 자연스럽게 진화할 것입니다. 오셔서 언제든 함께 논의합시다.

### README에 배지를 달았는데도 파일을 꼭 포함해야 하나요?
네. 진실의 원천(primary source of truth)으로서 `AI-DECLARATION.md` 파일을 포함할 것을 권장합니다. `README`에 있는 배지는 가볍게 훑어볼 수 있는 용도로, (A) `AI-DECLARATION.md` 파일이 존재함을 알리고, (B) 그 단계가 무엇인지 누구나 알아보기 쉽게 보여주는 역할을 할 뿐입니다.

### 로고는 무슨 의미인가요?
䷼ 주역의 64괘 중 61번째 괘인 '중부(中孚)' 괘입니다(유니코드: `U+4DFC`). ([출처](https://en.wikipedia.org/wiki/List_of_hexagrams_of_the_I_Ching#Hexagram_61))
