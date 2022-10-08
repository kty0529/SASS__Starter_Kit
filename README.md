# SASS_Starter_Kit
프로젝트를 진행할 때 반드시 포함하는 SASS 파일을 모아놓은 스타터 키트입니다.

개인적으로 사용하기 위해 만든 것이기 때문에 다른 스타일과 정상적으로 호환되지 않을 가능성이 크고 비정기적으로 깜짝 업데이트 됩니다.

<br>

## base
### 1. _reset.scss
브라우저가 모든 요소를 ​일관되게 렌더링하도록 스타일을 초기화 해줍니다.

### 2. _typography.scss
기본 폰트 스타일을 구성합니다.

<br>

## helpers
### 1. _index.scss
helpers 파일을 한번에 import 하는 용도로 사용하기 위해 만들었습니다.

### 2. _variables.scss
기본 폰트 크기, 색상, 반응형 기준 등의 전역 변수가 담겨있습니다.

### 3. _mixins.scss
재사용 사용할 속성이 모여있습니다.

### 4. _functions.scss
mixin으로 만들기 힘들거나 연산이 필요한 경우 등 조건이 다양한 경우에 대한 기능이 담겨있습니다.

<br>

## core.scss
위 파일들을 적절한 순서에 맞게 import 하여 compile 하는 대표 파일입니다.

<br>

## 기능 소개

### function `rem-calc()`
키트에서 사용중인 `rem-calc` 함수는 [Foundation](http://foundation.zurb.com/)의 기능을 가져와 입맛에 맞게 커스텀했습니다.

`rem-base`의 값에 따라 `rem`단위로 자동 변환되며 다음과 같이 사용할 수 있습니다.

| Before | After |
|--------|------|
| `padding: rem-calc(16);` | `padding: 1rem;` |
| `padding: rem-calc(16 16);` | `padding: 1rem 1rem;` |
| `padding: rem-calc(16 16 16);` | `padding: 1rem 1rem 1rem;` |
| `padding: rem-calc(16 16 16 16);` | `padding: 1rem 1rem 1rem 1rem;` |

또한, 단위를 입력해도 알아서 제거되고 rem으로 변경됩니다.

**예시)** `rem-calc(16px 8)` -> `1rem 0.5rem`
