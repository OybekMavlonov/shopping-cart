<template>
  <div
    class="products"
    @click="addToCart(product)"
  >
    <div class="products__img"></div>
    <div class="products__info">
      <div class="products__info-name">{{product.name}}</div>
      <div class="products__info-price">{{product.price}} So'm</div>
      <div class="products__info-number">{{product.number}}</div>
    </div>
  </div>
</template>

<script>
import EventBus from "../../EventBus";
export default {
  data() {
    return {
      show: true
    };
  },
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  methods: {
    addToCart(product) {
      EventBus.$emit("add-to-cart", product);
    }
  }
};
</script>

<style lang="scss">
.products {
  margin: 10px 0;
  padding: 16px;
  display: flex;
  background: #fff;
  border-radius: 4px;
  cursor: pointer;

  &__img {
    width: 50px;
    border: 1px solid #111;
    height: 50px;
  }

  &__info {
    margin-left: 15px;

    &-name {
      font-size: 14px;
      font-weight: 550;
    }

    &-price {
      display: inline;
      margin-top: 5px;
      margin-right: 45px;
      font-size: 13px;
      color: grey;
    }
    &-number {
      display: inline;
      margin-left: 45px;
      font-size: 13px;
      color: grey;
    }
  }
}
</style>