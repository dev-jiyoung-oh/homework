# 24.10.17 - Apple 제품 안내

## 결과 미리보기

- [완성본 페이지 방문 >>](https://dev-jiyoung-oh.github.io/homework/apple/apple.html)

![결과 화면 gif](./images/apple-result.gif)

<br/>

## 마크업&스타일링

### card 컴포넌트

```html
<div class="product-wrapper">
  <div class="product ipad-pro theme-blue">
    <p class="product-name">제품명</p>
    <p class="product-description">
      <span>설명(부제목)1</span>
      <span>설명(부제목)2</span>
    </p>
    <p class="product-open">출시일 관련 정보</p>
    <div class="product-btn-wrap">
      <a href="#" class="product-btn btn-default">더 알아보기</a>
      <a href="#" class="product-btn btn-outline">가격 보기</a>
    </div>
  </div>

  ...
</div>
```

```css
.product-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--small-spacing);
}

.product {
  grid-column: span 2;

  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;

  ...

  /* 테마 */
  &.theme-blue {
    color: var(--white);

    .product-btn {
      &.btn-default {...}
      &.btn-outline {...}
    }
  }
}

/* 반응형 */
@media (width >= 64rem) {
  .product {
    .product-description {
      ...
      span {
        display: inline;
      }
    }

    &.product-small {
      grid-column: span 1;
    }
    ...
  }
}
```
- 모바일 퍼스트(1024px 미만을 모바일, 1024px 이상을 데스크탑 환경으로 세팅)로 작성하였습니다.
- 스크린 너비에 따라 하나의 행에 표시되는 제품의 개수가 달라지므로 최대로 표시되는 제품의 수(이 경우 2개)에 맞게 그리드 컬럼을 나누었습니다.
- 기본적으로 제품은 한 행에 하나가 표시되므로 product 클래스의 "grid-column"값으로 "span 2"를 주었고, 데스크톱 환경일 때 해당하는 클래스(.product.product-small)는 "grid-column"값에 "span 1"을 주어 한 행에 두 제품이 표시되도록 하였습니다.
- 제품 설명(부제목)이 페이지 너비에 따라 달라지므로 p로 설명 요소(span)들을 감싸고, 모바일 환경에서는 span이 각각 다른 행에 표시되어야 하므로 "display"값을 "block"으로 하고 데스크톱 환경에서는 "display"값을 "inline"으로 하여 한 줄로 표현될 수 있도록 하였습니다.
- product 클래스에 테마 관련 클래스를 더해주어 각 테마에 맞는 글자 색상, 버튼 색상 등을 적용할 수 있도록 하였습니다.

<br/>

### 제품 이미지 처리
```css
.product {
  @media (max-resolution: 1x) {
    &.ipad-pro {
      background-image: url("./../../assets/apple/products/ipad_pro.jpeg");
    }
    &.iphone-15-pro {
      background-image: url("./../../assets/apple/products/iphone15_pro.jpeg");

      @media (width >= 64rem) {
        background-image: url("./../../assets/apple/products/iphone15_pro_wide.jpeg");
      }
    }
    ...
  }

  @media (min-resolution: 2x) {
    &.ipad-pro {
      background-image: url("./../../assets/apple/products/ipad_pro_2x.jpeg");
    }
    &.iphone-15-pro {
      background-image: url("./../../assets/apple/products/iphone15_pro_2x.jpeg");

      @media (width >= 64rem) {
        background-image: url("./../../assets/apple/products/iphone15_pro_wide_2x.jpeg");
      }
    }
    ...
  }
}
```
- 제폼 이미지를 CSS의 background 속성을 활용하여 구현하였습니다.
- 디바이스의 픽셀 밀도에 따라 보여지는 이미지를 다르게 하기 위하여 "resolution"특징을 이용하여 미디어 쿼리를 작성하였습니다.
- iphone 15 pro 제품의 경우 픽셀 밀도에 따라서도 이미지가 달라지지만, 스크린 너비에 따라서도 이미지가 달라지기 때문에 미디어 쿼리를 중첩해서 처리하였습니다.

<br/>

## 과제를 마치며

- 처음에 과제를 받았을 때는 막막했지만 이렇게 끝내고 보니 생각보다 많이 어렵지 않았던 것 같습니다. (물론 생각지 못한 점들이 있을 수도 있지만..)
- 수업시간에 배운 container 쿼리를 이용하여 반응형 레이아웃을 구현하고 싶었으나 지원하지 않는 브라우저가 있어 결국 미디어 쿼리를 이용하게 되었습니다. 업그레이드된 기술들이 얼른 모든 브라우저에 호환되어 해당 기술을 이용하여 개발할 수 있게 되면 좋겠습니다.
- 미디어 쿼리를 중첩해서 사용하지 않고 할 수 있는 방법이 있을지 궁금합니다.