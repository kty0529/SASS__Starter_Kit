# SASS_Starter_Kit
프로젝트를 진행할 때 반드시 포함하는 SASS 파일을 모아놓은 스타터 키트입니다.
<br>개인적으로 사용하기 위해 만든 것이기 때문에 다른 스타일과 정상적으로 호환되지 않을 가능성이 큽니다.

---

## base
### 1. _reset.scss
스타일을 초기화 해줍니다.

### 2. _grid.scss
Flexbox 기반 <u>[Grid 시스템](https://getbootstrap.com/docs/5.1/layout/grid/)</u>을 구성합니다.

### 3. _typography.scss
기본 폰트 스타일을 구성합니다.

<br>

## helpers
### 1. _variables.scss
전역 변수가 담겨있습니다.

### 2. _mixins.scss
재사용 사용할 속성이 모여있습니다.

### 3. _functions.scss
mixin으로 만들기 힘들거나 연산이 필요한 경우 등 조건이 다양한 경우에 대한 기능이 담겨있습니다.

### 4. _index.scss
helpers 파일을 한번에 불러올 수 있게 만들었습니다.

<br>

## core.scss
위 파일들을 적절한 순서에 맞게 import 하여 compile 하는 대표 파일입니다.
