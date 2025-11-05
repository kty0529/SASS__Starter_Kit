# SASS Starter Kit

![Sass Badge](https://img.shields.io/badge/Powered%20by-Sass-cc6699?logo=sass&logoColor=white)
![Stylelint Badge](https://img.shields.io/badge/Stylelint-14.16.1-263238?logo=stylelint&logoColor=white)
![License Badge](https://img.shields.io/badge/License-MIT-brightgreen)

> 반복되는 스타일 초기 세팅을 단 한 번의 `@use`로 해결하는 SCSS 스타터 키트입니다.

---

## 프로젝트 한눈에 보기
| 항목 | 내용 |
| ---- | ---- |
| 엔트리 포인트 | `scss/core.scss` |
| 주요 폴더 | `scss/base`, `scss/helpers`, `css/` |
| 스크립트 | `npm run watch`, `npm run lint` |
| 린터 규칙 | `stylelint-config-idiomatic-order`, `stylelint-config-recommended-scss` |
| 라이선스 | MIT License |

---

## 소개
이 저장소는 프로젝트 시작 시 반복적으로 세팅하는 SCSS 초석을 빠르게 불러오기 위한 템플릿입니다. `core.scss` 한 파일만 포함하면 reset, typography, color 시스템과 자주 쓰는 믹스인이 한 번에 준비됩니다.

**주요 특징**
- `@use` 기반의 모듈식 구조로 부분 파일 간 의존성을 명확히 관리합니다.
- 플랫 컬러 팔레트와 반응형 브레이크포인트가 미리 정의되어 빠른 커스터마이징이 가능합니다.
- 실무에서 자주 쓰이는 레이아웃/유틸리티 믹스인을 문서화된 형태로 제공합니다.

---

## 빠른 시작
1. 패키지 설치: `npm install`
2. 개발 모드: `npm run watch`
   - 내부적으로 `sass --watch scss:css`가 실행되어 `scss/` 변경을 실시간으로 `css/`에 반영합니다.
3. 출력 경로를 바꾸고 싶다면 `package.json`의 `watch` 스크립트를 수정하세요.

```json
"watch": "sass --style=compressed --watch scss:dist/css"
```

---

## 디렉터리 구조
```
SASS__Starter_Kit/
  scss/
    base/                // reset, typography, colors
    helpers/             // variables, mixins, index
    core.scss            // 최종 진입점
  css/                   // Sass 컴파일 결과물
  AGENTS.md              // 팀 가이드라인
  package.json
  .stylelintrc.json
```

---

## 핵심 모듈 안내
- **base**: 브라우저 초기화(`_reset.scss`), 타이포 스타일(`_typography.scss`), 컬러 헬퍼(`_colors.scss`).
- **helpers**: 재사용 가능한 토큰과 믹스인을 제공하는 핵심 라이브러리 영역입니다.
  - `_variables.scss`: `$theme-colors` 팔레트, 컨테이너 최대 폭과 `gutter`, `map.get` 기반 반응형 브레이크포인트를 선언합니다. 브랜드 컬러나 레이아웃 폭을 커스터마이징하려면 이 파일에서 값을 변경하세요.
  - `_mixins.scss`: `fullscreen`, `absolute`, `hide-scrollbar`, `px-to-vw`, `container` 등 시맨틱 레이아웃과 유틸리티 믹스인을 모아두고 각 파라미터 기본값을 주석으로 안내합니다. 새 믹스인을 추가할 때도 이 파일에 문서화를 함께 남깁니다.
  - `_index.scss`: 변수와 믹스인을 다시 export해 `@use "./helpers" as *` 한 줄로 전역 토큰을 불러올 수 있게 합니다.
  - 사용 예:
    ```scss
    @use "./helpers" as *;

    .container {
      @include container();
    }

    .card-title {
      color: map.get($theme-colors, 'primary');
    }
    ```
- **core.scss**: base와 helpers를 지정된 순서로 불러오고, 이후 추가한 기능성 partial을 연결하는 허브입니다.

---

## 개발 워크플로
> **TIP** 새로운 partial을 만들었다면 `core.scss`에 `@use`를 추가해 워처가 인식하도록 하세요.

- `css/`는 자동 생성 폴더입니다. 수동 편집 대신 SCSS에서 변경하세요.
- 브레이크포인트 추가나 색상 팔레트 변경은 `helpers/_variables.scss`에서 관리합니다.
- 변경 후 `npm run lint` 및 `npm run watch`를 실행해 스타일 가이드 준수와 컴파일 정상 여부를 확인합니다.

---

## 스타일 가이드 & 린트
- 모든 SCSS는 두 칸 들여쓰기를 사용하며, 속성 순서는 `stylelint-config-idiomatic-order` 규칙을 따릅니다.
- `npm run lint`로 Stylelint를 실행하고, 필요한 경우 `npx stylelint "scss/**/*.scss" --fix`로 자동 정렬하세요.
- `.stylelintrc.json`은 `stylelint-config-recommended-scss`를 상속하므로 Sass 전용 문법 검사도 함께 진행됩니다.
- 경고가 해결되지 않을 경우 주석으로 무시하기보다 변수/믹스인 재활용을 통해 구조적 개선을 시도하세요.

---

## 믹스인 레퍼런스
### 요약 표
| 믹스인 | 용도 | 기본 인자 |
| ------ | ---- | ---------- |
| `fullscreen` | 전체 화면 레이어 | `$z: 1`, `$p: "absolute"` |
| `absolute` | 요소 정렬 제어 | `$p: "center"` |
| `disable` | 인터랙션 비활성화 | `$boolean: "true"` |
| `text-ellipsis` | 한 줄 말줄임 | - |
| `box-ellipsis` | 다중 라인 말줄임 | `$line: 3`, `$lineHeight: 20px`, `$boxHeight: "auto"` |
| `hide-scrollbar` | 스크롤바 숨김 | - |
| `px-to-vw` | 반응형 단위 변환 | `$property`, `$value`, `$max-width`, `$important` |
| `container` | 공통 레이아웃 폭 | - |

> 아래는 각 믹스인에 대한 상세 설명과 예시 코드입니다.

### `fullscreen($z: 1, $p: "absolute")`
- 요소를 화면 전체에 채워 넣습니다. `z-index`와 `position`을 동시에 제어합니다.
- 모달 배경처럼 전체 화면이 필요한 경우 사용하세요.
```scss
@use "./helpers" as *;

.modal-backdrop {
  @include fullscreen(20, "fixed");
  background: rgba(0, 0, 0, 0.6);
}
```

### `absolute($p: "center")`
- 요소를 떠 있게 만들고 정렬 방향을 선택합니다. `center`, `vertical`, `horizontal`을 지원합니다.
```scss
.tooltip {
  width: 180px;
  height: auto;
  @include absolute("horizontal");
}
```

### `disable($boolean: "true")`
- 사용자 상호작용을 비활성화합니다. 반응형 조건에 따라 다시 활성화할 수 있습니다.
```scss
.button {
  @include disable();

  @media ($md_down) {
    @include disable(false);
  }
}
```

### `text-ellipsis()`
- 한 줄 말줄임 처리를 적용합니다.
```scss
.title {
  max-width: 240px;
  @include text-ellipsis();
}
```

### `box-ellipsis($line: 3, $lineHeight: 20px, $boxHeight: "auto")`
- 여러 줄 말줄임을 지원합니다. `$boxHeight`를 `"fixed"`로 지정하면 고정 높이가 설정됩니다.
```scss
.card-description {
  @include box-ellipsis(4, 18px);
}

.card-description--fixed {
  @include box-ellipsis(3, 22px, "fixed");
}
```

### `hide-scrollbar()`
- 스크롤바 시각 요소를 숨깁니다. 스크롤 자체는 유지합니다.
```scss
.side-nav {
  overflow-y: auto;
  @include hide-scrollbar();
}
```

### `px-to-vw($property, $value, $max-width: map.get($grid-breakpoints, "md"), $important: false)`
- 픽셀 단위를 뷰포트 폭 기반 값으로 변환합니다. `$max-width`를 조정해 전환 기준을 변경할 수 있습니다.
```scss
.hero {
  @include px-to-vw(padding, 60px 120px, 1440px);
}

.hero__title {
  @include px-to-vw(font-size, 32px, $important: true);
}
```

### `container()`
- `$container`와 `$gutter` 값을 활용해 공통 레이아웃 폭을 정의합니다.
```scss
.page-container {
  @include container();
}
```

### Breakpoints 활용 예시
- `_variables.scss`에 선언된 `$md_up`, `$md_down` 등 미디어 쿼리 토큰을 사용하는 패턴입니다.
```scss
@use "./helpers" as *;

.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;

  @media ($md_down) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media ($sm_down) {
    grid-template-columns: 1fr;
  }
}
```

---

## 커스터마이징 가이드
- **컬러 팔레트 변경**: `helpers/_variables.scss`의 `$theme-colors` 맵을 수정해 글로벌 테마 색상을 재정의합니다. 필요 시 새로운 키를 추가하고 `_colors.scss`에서 매칭되는 유틸리티 클래스를 확장하세요.
- **레이아웃 폭 조정**: `$container`와 `$gutter` 값을 수정하면 `@include container()` 믹스인의 최대 폭과 내부 여백이 즉시 반영됩니다.
- **브레이크포인트 추가/수정**: `$grid-breakpoints` 맵에 새 키를 추가한 뒤 `map.get`으로 접근하면 반응형 미디어 쿼리에 활용할 수 있습니다.
- **빌드 경로 커스터마이징**: 프로젝트 구조가 다르다면 `package.json`의 `watch` 스크립트를 원하는 입력/출력 경로로 변경하거나 `--style=compressed` 옵션을 추가해 압축 결과물을 얻을 수 있습니다.
- **프로젝트별 Partial 추가**: `scss/` 하위에 새 디렉터리를 만든 뒤 partial을 작성하고, `core.scss`에 `@use "./새경로/partial" as *;`를 추가해 빌드 체인에 연결합니다.

---

## 문제 해결 & FAQ
> **NOTE** Sass CLI는 오류 발생 시 전체 빌드를 중단하므로 터미널 메시지를 항상 확인하세요.

- **CSS가 갱신되지 않아요.**
  - 워처가 실행 중인지 `npm run watch` 터미널을 확인하고, 필요 시 프로세스를 재시작하세요.
  - SCSS에서 오류가 발생하면 Sass가 컴파일을 중단합니다. 터미널 로그의 오류 위치를 수정한 뒤 다시 저장하세요.
- **Stylelint가 지나치게 오래 걸립니다.**
  - `npx stylelint "scss/**/*.scss" --cache` 옵션으로 캐시를 활성화하면 반복 실행 속도를 개선할 수 있습니다.
- **px-to-vw가 기대와 다르게 작동합니다.**
  - 기본 최대 폭은 `$grid-breakpoints`의 `md` 값입니다. 특정 컴포넌트에서 다른 기준을 사용하려면 `@include px-to-vw(font-size, 16px, 1440px);`처럼 세 번째 인자를 지정하세요.
- **Node 버전은 무엇이 필요한가요?**
  - Dart Sass와 Stylelint는 LTS 버전(Node 16 이상)에서 테스트되었습니다. 구버전에서는 설치 오류가 발생할 수 있습니다.

---

## 라이선스 & 참고
이 스타터 키트는 MIT License로 배포됩니다. 자유롭게 포크하고 수정·재배포할 수 있으며, 라이선스 전문은 [MIT License](https://opensource.org/licenses/MIT)를 참고하세요. 필요한 경우 프로젝트 요구에 맞춰 마음껏 커스터마이징해 활용하셔도 됩니다.
