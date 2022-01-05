# ✨SASS✨

[`참고`](https://www.notion.so/23157e6484a64582853c7867f9b88150?v=492e2c8d7a8e4e369c8badfecc5c6676)

## 정의
> - 스타일시트를 더 쉽게 사용하고자 등장한 스타일시트 엔진(특정한 형태의 스타일시트를 CSS 스타일 시트로 변경해주는 변환 엔진 컴파일러). 브라우저가 이해할 수 있는 CSS로 변환해주는 도구이다.
> - 브라우저가 SASS를 직접 로딩하는 것이 아니라 개발은 SASS를 기반으로 한 후, CSS로 익스포트하는 과정을 거치기 때문에 SASS는 CSS 전처리기의 하나이다.

## 사용 목적
> 1. 스타일시트가 복잡해짐에 따라 유지관리를 용이하게 하기 위함 (코드 재사용 가능)
> 2. 변수, 네이스팅, 믹스인, 가져오기, 상속, 내장기능 등 CSS에는 없는 편의 기능들이 존재하여 시간 절약 가능

## 내용 정리

<details>
<summary> [1] 파일 분리와 Nesting</summary>
<div markdown="1">
<br/>
📌 파일 분리  
<br/><br/>
<img src="https://user-images.githubusercontent.com/58348662/147869832-7f0b5331-3927-4887-bbac-782e16dab4e1.png" width="500">
  
> (1) 프레임 별 scss 파일 - `언더바(_)` 사용  
  : `언더바(_)`를 붙이지 않으면 분할 된 파일들도 모두 컴파일되면서 `.css` 파일이 나눠서 저장되기 때문에 `.scss` 파일 이름 앞에 '_'를 붙여 저장한다. 이렇게 하면 Sass에게 이 파일이 main 파일의 일부분임을 알려줘서 해당 파일은 `.css` 파일로 컴파일하지 않고 내부에서 `@import` 형태로 작동하게 된다.  
  
> (2) 메인 scss 파일  
  : 분할된 `.scss` 파일을 import 하는 용도로 사용되며, 컴파일 시 `.css` 파일이 자동으로 생성된다.


📌 Nesting
  > 기존 CSS는 부모에게 상속된 자식 요소에 스타일을 적용할 때 매번 최상위 선택자를 반복 선언해야 된다는 문제가 있지만, 중첩을 사용하면 최상위 선택자를 한 번만 선언하여도 되기에 코드의 반복을 줄일 수 있다.
  ```css
  /* CSS */
  info-list div {
    display: flex;
    font-size: 14px;
    color: #4f4f4f;
  }
  info-list div dt {
    font-weight: 700;
    margin-right: 7px;
  }
  ```
  ```scss
  /* SCSS */
  info-list {
    div {
      display: flex;
      font-size: 14px;
      color: #4f4f4f;
      dt {
        font-weight: 700;
        margin-right: 7px;
      }
    }
  }
  ```
  
  (1) 속성 Nesting
  ```scss
  .add-icon {
    background : {
      image: url("./image.png");
      position: center center;
      repeat: no-repeat;
      size: 14px 14px;
    }
  }
  ```
  
  (2) Ampersand(&)
  ```scss
  .box {
  // 가상선택자
    &:focus{} 
    &:hover{}
    &:active{}
    &:first-child{}
    &:nth-child(2){}
  // 가상요소
    &::after{} 
    &::before{}
  // 공통 클래스명 중첩
    &-red { background: #ffd700; }
    &-yellow { background: #ff6347; }
  }
  ```
  
  (3) @at-root
  : 중첩에서 벗어나고 싶은 선택자 앞에 작성
  ```scss
  .article-content {
    font-size: 14px;
    opacity: 0.7;
    @at-root i {
      opacity: 0.5;
    }
  }
  ```

</div>
</details>

<!---------------------------------------------------------------------------------------------------------------->

<details>
<summary>[2] 변수 (Variable)</summary>
<div markdown="1">
  <br/>
📌 변수 생성 및 사용 : `$`
  
```scss
$bgColor: #FFF;
$font-p: 13px;
$base-font: 'Noto Sans KR', sans-serif;

body {
  background-color: $bgColor;
  font-size: $font-p;
  font-family: $base-font;
}
```
  
📌 TYPE  
  
  |type|ex|
  |:-:|------|
  |numbers|1, .82, 20px, 2em|
  |strings|"./images/a.png", bold, left, uppercase|
  |colors|green, #FFF, rbga(255,0,0,.5)|
  |booleans|true, false|
  |null|null|
  |lists|$sizes: 10px 12px 16px|
  |maps|$weights: ("r":400, "m":500, "b":700)|
  

📌 Lists, Maps
  - Lists
  > `,`, ` `, `/` 로 구분하여 작성  
  index 값이 0이 아닌 1부터 시작하며, -1은 마지막 index를 가르킴  
  
|function|description|
|:-:|-----|
|append(list, value, [separator])|lists의 값을 추가|
|index(list, value)|lists의 값에 대한 인덱스를 리턴|
|nth(list, n)|lists의 n번째 인덱스에 해당하는 값 리턴|
  
  - Maps
  > `(키:값, 키:값, ...)` 형태로 저장하여 사용

|function|description|
|:-:|-----|
|map-get(map,key)|키에 해당하는 값을 리턴|
|map-keys(map)|map에 들어있는 키를 전부 리턴|
|map-values(map)|map에 들어있는 값 전부 리턴|
  
📌 SCOPE
  - local
  > 선언한 자신을 감싸고 있는 중괄호 안에서 사용되며, 하위 단계에 있는 중괄호 안에서도 사용 가능 (뒤에 !global을 붙여 전역변수로 변경 가능)
  - global
  > 가장 윗부분에 정의함으로써 파일 내에 어디서든 사용 가능
  
📌 OPERATOR
  > 1. 비교연산자 - 숫자 ( `<`, `<=`, `>`, `>=` `==`, `!=` )  
  > 2. 산술연산자 - 숫자/색 ( `+`, `-`, `*`, `/`, `%` )  
  > 3. 문자열 ( `a+b` )  
  > 4. 논리연산자 ( `not`, `and`, `or` )  

</div>
</details>


<!---------------------------------------------------------------------------------------------------------------->



<details>
<summary>[3] Mixin</summary>
<div markdown="1">
  <br/>

> 코드를 재사용하기 위해 만들어진 기능
```scss
@mixin 이름(매개변수) {  // 생성
  // 중복되는 코드
}
@include 이름(인수) // 사용
```

  📌 Default Value  
  ```scss
  @mixin flexCenter($size : 10px) {
  display: flex;
  justify-content: center;
  align-items: center;
    li {
      margin-right: $size;
    }
}
  ```
  
  📌 Content  
  > `@content`를 사용하면 원하는 부분에 스타일을 추가하여 전달할 수 있다.
  ```scss
  @mixin flexCenter {
    display: flex;
    justify-content: center;
    align-items: center;
    @content
  }
  .card {
    @include flexCenter{ color: white; };
  }
  ```
  
</div>
</details>



<!---------------------------------------------------------------------------------------------------------------->



<details>
<summary>[4] Extend</summary>
<div markdown="1">
<br/>

> 연관 있는 선택자들에 동일한 소스코드를 적용하기 위함 (mixin은 연관 없는 선택자에서 조금 다른 스타일을 적용하기 위함)
  
📌 Class 이름 가져오기
```scss
  .profile-user {
    background-image: url('./profile.png');
    background-size: cover;
    background-position: 50% 50%;
    border-radius: 50%;
    width: 50px;
    height: 50px;
  }
  
  .comment-user {
    @extend .profile-user;
  }
```
  
  
📌 Placeholder(%) 사용하기
  > %선택자는 CSS로 컴파일되지 않는다. (class보다 %사용을 권장)
```scss
  %base-button {
    width: 133px;
    height: 44px;
    border-radius: 10px;
  }
  
  .btn-1 {
    @extend %base-button;
    background-color: #FFF;
    color: #ff375f;
    border: 3px solid #ff375f;
  }
  
  .btn-2 {
    @extend %base-button;
    background-color: #ff375f;
    color: white;
  }
```
  
  
</div>
</details>




<!---------------------------------------------------------------------------------------------------------------->



<details>
<summary>[5] 조건문, 반복문, 함수</summary>
<div markdown="1">
<br/>
📌 조건문  
  
1. if 문
```scss
  @if (조건) {
    // 조건이 참일 때 실행될 구문, 소괄호 생략 가능
  }
```
2. else 문
```scss
  @if (조건) {
    // 조건이 참일 때 실행될 구문
  } @else {
    // if문의 조건이 거짓일 때 실행될 구문
  }
```
3. if-else 문
```scss
  @if (조건) {
    // 조건이 참일 때 실행될 구문
  } @else if (조건) {
    // else if 조건이 참일 때 실행될 구문
  } @else {
    // 위 모든 조건이 거짓일 때 실행될 구문
  }
```
  
📌 반복문  
1. for 문
```scss
  @for ($변수) from (시작) through (끝) {
    // 반복할 내용
    // 변수 사용 시 `#{$변수}` 형태로 작성
  }
```
2. each 문
```scss
  @each ($변수) in (리스트or맵) {
    // 반복할 내용
  }
```
3. while 문
```scss
  @while 조건 {
    // 반복할 내용
  }
```
  
📌 함수  
1. function
```scss
  @function 함수이름 ($매개변수) {
    // 실행 코드
    @return 값
  }
```
2. 내장함수  

(1) 색상 함수  
  
|function|description|
|--|-----|
|lignten(color, amount)|기존 색상의 밝기를 높임(0%-100%)|
|darken(color, amount)|기존 색상의 밝기를 낮춤(0%-100%)|
|mix(color1, color2, weight)|2개의 색상을 섞어서 새로운 색상을 만듦|
  
(2) 숫자 함수  
  
|function|description|
|--|-----|
|max(number, ..)|괄호에 넣은 값 중 가장 큰 수를 반환|
|min(number, ..)|괄호에 넣은 값 중 가장 작은 수를 반환|
|percentage(number)|퍼센트로 숫자를 바꿈|
|comparable(num1, num2)|num1과 num2가 비교 가능한지 확인 후 true/false 값 반환|
  
(3) 문자 함수  
  
|function|description|
|--|-----|
|str-insert(string, insert, index)|문자열에 원하는 위치(index)에 문자를 넣은 후 새로운 문자열 반환|
|str-index(string,substring)|문자열에서 해당 문자의 index 값을 반환|
|to-upper-case(string)|문자열 전부를 대문자로 바꿔줌|
|to-lower-case(string)|문자열 전부를 소문자로 바꿔줌|
  
(4) 확인 함수  
  
|function|description|
|--|-----|
|unit(number)|숫자의 단위를 반환해줌|
|unitless(number)|단위를 가지고 있는지 판단하여 true/false 값을 반환|
|variable-exists(name)|변수가 현재 범위에 존재하는지 판단하여 true/flase 값을 반환. 이 함수의 인수는 `$`없이 사용|

  
</div>
</details>
