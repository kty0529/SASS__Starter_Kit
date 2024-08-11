# SASS_Starter_Kit
프로젝트를 진행할 때 반드시 포함하는 SASS 파일을 모아놓은 스타터 키트입니다.

개인적으로 사용하기 위해 만든 것이기 때문에 다른 스타일과 정상적으로 호환되지 않을 가능성이 크고 비정기적으로 **깜짝🎉** 업데이트됩니다.
<br>참고용으로 봐주세요.


<br>


## Install

```
npm run install
npm run watch
```

build /scss -> /css


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

호출할 땐 `_index.scss`의 선언은 생략해도 됩니다.
```scss
@import '/scss/helpers';
```

### _variables.scss
기본 폰트 크기, 색상, 반응형 기준 등의 전역 변수가 담겨있습니다.

### _mixins.scss
재사용 사용할 속성이 모여있습니다.

#### 1. px to vw
```scss
// 사용 예시
.element {
  margin: 0 auto 0;
  padding: 0 7px;
  font-size: 16px;
  grid-template-columns: 1fr 2fr;
  width: auto;

  // !important가 없는 경우
  @include px-to-vw(margin, 0 auto 0);
  @include px-to-vw(padding, 0 7px);
  @include px-to-vw(grid-template-columns, 1fr 2fr);
  @include px-to-vw(width, auto);

  // !important가 있는 경우
  @include px-to-vw(font-size, 16px, 1440px, true);

  // $max-width를 수정하지 않고 !important만 사용해야 하는 경우
  @include px-to-vw(font-size, 16px, $important: true);
}
```

<br>

## core.scss
`/base`와 `/helpers`의 파일을 적절한 순서에 맞게 불러와 최종 compile 하는 파일입니다.
