# ✨SASS✨

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
 

</div>
</details>

