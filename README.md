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

빌드 위치를 변경하기 위해선 package.json의 `"watch": "sass --watch scss:css"` 내용을 변경하면 됩니다.
<br>ex) `"watch": "sass --style=compressed --update --watch theme02/wp-content/themes/theme02/assets/scss/:theme02/wp-content/themes/theme02/assets/css/"`
<br>옵션 관련은 [sass lang 공식 홈페이지](https://sass-lang.com/documentation/cli/dart-sass/)에서 확인하면 됩니다.

<br>

## base

### 1. \_reset.scss

브라우저에서 모든 요소를 ​일관되게 보여주도록 스타일을 초기화 해줍니다.

### 2. \_typography.scss

`strong`, `heading` 등 문단 관련 공통 스타일을 관리합니다.

### 3. \_colors.scss

`/helpers/_variables.scss`에 정의된 `$theme-colors`를 기반으로 '글자색', '배경색'을 지정할 수 있는 기본 class가 선언되어있고 색상 관련 스타일을 관리하기 위해 추가했습니다.

```html
<span class="text-primary">글자색 #2c3e50</span>
<div class="bg-info">배경색 #3498db</div>
```

<br>

## helpers

필요한 곳에서 `@use './helpers/mixins' as *`를 선언해서 전체 호출하거나 필요한 값만 가져다 사용하면 됩니다.

### 1. \_variables.scss

기본 폰트 크기, 색상, 반응형 기준 등의 전역 변수가 담겨있습니다.

### 3. \_mixins.scss

재사용 가능한 속성을 모아두었습니다.

#### fullscreen

화면 전체에 꽉 차게 만듭니다.

```scss
// @params($z: 1, $p, 'absolute')
// $z: z-index / 1~n (숫자)
// $p: position / absolute, fixed

@include fullscreen(1);
@include fullscreen(2, "fixed");
```

#### absolute

요소를 공중에 띄우며 `$p` 값을 기준으로 정렬합니다.
<br>이 mixin이 적용된 요소는 `width`, `height`값이 필요합니다.

```scss
// @params($p: 'center')
// $p: position / center(정중앙), vertical(세로중앙), horizontal(가로중앙)

@include absolute();
@include absolute("vertical");
```

#### disable

사용자의 클릭(또는 터치) 액션 및 선택을 막습니다.

```scss
// @params($boolean: 'true')
// $boolean: 'true', 'false'

.element {
  @include disabled();

  @media ($md_down) {
    @include disabled("false");
  }
}
```

#### text-ellipsis

한 줄 말줄임 처리를 합니다.

```scss
.element {
  @include text-ellipsis();
}
```

#### box-ellipsis

여러 줄 말줄임 처리를 합니다. 파라미터를 변경해 원하는 크기로 맞출 수 있고 박스 크기를 자유롭게 하거나 고정 값으로 설정할 수 있습니다.

```scss
// @params($line: 3, $lineHeight: 20px, $boxHeight: 'auto')
// $line: 1~n (숫자)
// $lineHeight: 00px
// $boxHeight: 'auto', 40px

.element {
  // line-height가 20px인 글을 3줄 표시 후 말줄임, 박스 높이 지정 값으로 고정
  @include box-ellipsis(3, 20px, 60px);

  // 박스 최대 높이 제한, 최대 높이를 넘지 않는 글은 말줄임 처리 안함, 박스 크기 유동적
  @include box-ellipsis(3, 20px);
}
```

#### hide-scrollbar

스크롤바 외형을 숨겨줍니다.

```scss
.element {
  @mixin hide-scrollbar();
}
```

#### px to vw

반응형 작업 중, 비율에 맞게 줄어들어야 하는 랜딩 페이지 등을 만들어야 하는 경우를 대비해 px 을 vw 단위로 변환해주는 mixin 입니다.
<br> 기준이 되는 `$max-width`는 `helper/variables`의 `$grid-breakpoints`의 `md`값을 기준으로 합니다.

```scss
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
