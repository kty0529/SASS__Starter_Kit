# SASS_Starter_Kit
프로젝트를 진행할 때 반드시 포함하는 SASS 파일을 모아놓은 스타터 키트입니다.

개인적으로 사용하기 위해 만든 것이기 때문에 다른 스타일과 정상적으로 호환되지 않을 가능성이 크고 비정기적으로 **깜짝🎉** 업데이트됩니다.
<br>참고용으로 봐주세요.


<br>

## base
### _reset.scss
브라우저에서 모든 요소를 ​일관되게 보여주도록 스타일을 초기화 해줍니다.

### _typography.scss
`strong`, `heading` 등 문단 관련 공통 스타일을 관리합니다.

### _colors.scss
`/helpers/_variables.scss`에 정의된 `$theme-colors`를 기반으로 "글자색", "배경색"을 지정할 수 있는 기본 class가 선언되어있고
색상 관련 스타일을 관리할 수 있습니다.

```html
<span class="text-primary">글자색 #2c3e50</span>
<div class="bg-info">배경색 #3498db</div>
```

<br>

## helpers
### _index.scss
helpers 파일을 한번에 import 하는 용도로 사용하기 위해 만들었습니다.

```scss
@import '/scss/helpers';
```

### _variables.scss
기본 폰트 크기, 색상, 반응형 기준 등의 전역 변수가 담겨있습니다.

### _mixins.scss
재사용 사용할 속성이 모여있습니다.

### _functions.scss
단순 재사용이 아닌 기능이 동작하는 속성들을 관리합니다.

<br>

## core.scss
`/base`와 `/helpers`의 파일을 적절한 순서에 맞게 불러와 최종 compile 하는 파일입니다.

<br>

## 기능 소개

### `rem-calc()`
**px**을 **rem**으로 변환해주는 함수입니다.
<br>[Foundation](http://foundation.zurb.com/)에서 제공하는 코드를 Kit에 맞게 일부 수정해서 사용중입니다.

`_variables.scss/$rem-base`의 값에 따라 `rem`단위로 자동 계산되며 다음과 같이 사용할 수 있습니다.

| Before | After |
|--------|------|
| `padding: rem-calc(16);` | `padding: 1rem;` |
| `padding: rem-calc(16 16);` | `padding: 1rem 1rem;` |
| `padding: rem-calc(16 16 16);` | `padding: 1rem 1rem 1rem;` |
| `padding: rem-calc(16 16 16 16);` | `padding: 1rem 1rem 1rem 1rem;` |

⭐️ 단위를 입력해도 알아서 제거되고 `rem`으로 변경됩니다.

**예시)** `rem-calc(16px 16)` -> `1rem 1rem`
