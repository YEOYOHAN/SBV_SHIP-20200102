<template>
<div id="product-carousel-container">
  <ul id="product-carousel">
    <li class="item-1">
      <img src="https://images.prd.dlivecdn.com/category/h4wbkz4xem5jw3ueqsz">
    </li>
    <li class="item-2">
      <img src="https://gameplanet-53f8.kxcdn.com/media/catalog/product/cache/4/thumbnail/9df78eab33525d08d6e5fb8d27136e95/f/i/fifa-20-champions-generica.jpg">
    </li>
    <li class="item-3">
      <img src="http://www.koreanculture.org.au/wp-content/uploads/2019/11/coming-soon.jpg">
    </li>
    <li class="item-4">
      <img src="http://www.koreanculture.org.au/wp-content/uploads/2019/11/coming-soon.jpg">
    </li>
    <li class="item-5">
      <img src="https://image.shutterstock.com/z/stock-vector-soccer-or-football-player-running-on-the-field-concept-flyer-and-abstract-poster-vector-540031792.jpg">
    </li>
  </ul>

  <div id="product-carousel-nav">
    <button class="carousel-nav prev"></button>
    <button class="carousel-nav next"></button>
  </div>
  <div id="carousel-dots">
    <ul>
      <li class="active"></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  </div>
</div>
</template>
<script>
import $ from 'jquery'
export default {
  mounted() {
const $carousel_cells = $('#product-carousel li');
const $carousel_dots = $('#carousel-dots li');
const $carousel_nav = $('.carousel-nav');
let selected_product_index = 0;

function selectProduct(index) {
  selected_product_index = index % $carousel_cells.length;

  if (selected_product_index < 0) selected_product_index = $carousel_cells.length + selected_product_index;

  $carousel_cells.each(function(i) {
    let offset = i - selected_product_index;
    if (offset < 0) offset += $carousel_cells.length;

    let index;
    for (index = 0; index < $carousel_cells.length + 1; index++) {
      $(this).removeClass('item-' + index).addClass('item-' + (offset + 1));
    }
  });

  $carousel_dots.eq(index).addClass('active').siblings('li').removeClass('active');
}

/* Arrow clicks */
$carousel_nav.click(function() {
  const delta = $(this).hasClass('prev') ? -1 : 1;
  const $delta_product = $(`#product-carousel li:eq(${(selected_product_index + delta) % $carousel_cells.length})`);
  const delta_product_index = parseInt($delta_product.index());
  selectProduct(delta_product_index);
});

/* Can clicks */
$carousel_cells.click(function () {
  selectProduct($(this).index());
});

/* Pagination */
$carousel_dots.click(function (e) {
  selectProduct($(this).index());
  $(e.currentTarget).addClass('active').siblings('li').removeClass('active');
});

/* Left/Right key arrows */
$(document).keydown(e => {
  const delta = e.keyCode == 37 ? -1  : 1;
  const $delta_product = $(`#product-carousel li:eq(${(selected_product_index + delta) % $carousel_cells.length})`);
  const delta_product_index = parseInt($delta_product.index());

  if ((e.keyCode == 37) || (e.keyCode == 39)) {
    selectProduct(delta_product_index);
    return false;
  }
});

/*
Inspired by:
https://www.7up.com/en/products
*/
  }
}
</script>
<style scoped>
#product-carousel-container {
  position: relative;
  width: 50%;
  margin: auto;
}

#product-carousel {
  height: 45vw;
  margin: 50px 0 0;
  list-style: none;
  position: relative;
}
#product-carousel li {
  position: absolute;
  left: 50%;
  top: 0;
  width: 30%;
  height: 100%;
  padding: 0;
  cursor: pointer;
  transition: -webkit-transform 1.3s cubic-bezier(0.19, 1, 0.22, 1);
  transition: transform 1.3s cubic-bezier(0.19, 1, 0.22, 1);
  transition: transform 1.3s cubic-bezier(0.19, 1, 0.22, 1), -webkit-transform 1.3s cubic-bezier(0.19, 1, 0.22, 1);
  z-index: 1;
}
#product-carousel li.item-1 {
  z-index: 2;
  -webkit-transform: translateX(-50%) scale(1) translate3d(0, 0, 0);
          transform: translateX(-50%) scale(1) translate3d(0, 0, 0);
}
#product-carousel li.item-2 {
  z-index: 1;
  -webkit-transform: translateX(-50%) scale(0.7) translate3d(240%, -10%, 0);
          transform: translateX(-50%) scale(0.7) translate3d(240%, -10%, 0);
}
#product-carousel li.item-3 {
  z-index: 0;
  -webkit-transform: translateX(-50%) scale(0.5) translate3d(180%, -31%, 0);
          transform: translateX(-50%) scale(0.5) translate3d(180%, -31%, 0);
}
#product-carousel li.item-4 {
  z-index: 0;
  -webkit-transform: translateX(-50%) scale(0.5) translate3d(-180%, -31%, 0);
          transform: translateX(-50%) scale(0.5) translate3d(-180%, -31%, 0);
}
#product-carousel li.item-5 {
  z-index: 1;
  -webkit-transform: translateX(-50%) scale(0.7) translate3d(-240%, -10%, 0);
          transform: translateX(-50%) scale(0.7) translate3d(-240%, -10%, 0);
}
#product-carousel li:after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  display: block;
  width: 100%;
  height: 100%;
  background: url(https://www.7up.com/images/bottle-shadow.png) no-repeat 50% 85%;
  background-size: 100% auto;
}
#product-carousel li:hover img {
  -webkit-transform: translateY(-15px);
          transform: translateY(-15px);
}
#product-carousel li:not(:hover) img {
  transition: -webkit-transform .075s ease-out;
  transition: transform .075s ease-out;
  transition: transform .075s ease-out, -webkit-transform .075s ease-out;
}
#product-carousel li img {
  width: 100%;
  height: auto;
  margin-top: 50%;
  transition: -webkit-transform .25s ease-in;
  transition: transform .25s ease-in;
  transition: transform .25s ease-in, -webkit-transform .25s ease-in;
}

#product-carousel-nav .carousel-nav {
  position: absolute;
  top: 45%;
  width: 50px;
  height: 50px;
  border-top: 2px solid #009e5f;
  border-right: 2px solid #009e5f;
  border-bottom: none;
  border-left: none;
  background-color: transparent;
  outline: 0;
  cursor: pointer;
}
#product-carousel-nav .carousel-nav.prev {
  left: -35%;
  -webkit-transform: rotate(-135deg);
          transform: rotate(-135deg);
}
#product-carousel-nav .carousel-nav.next {
  right: -35%;
  -webkit-transform: rotate(45deg);
          transform: rotate(45deg);
}

#carousel-dots {
  position: absolute;
  bottom: 0;
  width: 100%;
  z-index: 2;
}
#carousel-dots ul {
  display: flex;
  justify-content: center;
  margin-bottom: 50px;
}
#carousel-dots ul li {
  display: inline-block;
  margin: 0 15px;
  width: 10px;
  height: 10px;
  background-color: #ccc;
  border-radius: 100%;
  cursor: pointer;
}
#carousel-dots ul li.active {
  background-color: #009e5f;
}
</style>