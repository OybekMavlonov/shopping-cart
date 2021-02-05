<template>
  <div class="col-md-9">
    <div class="row">
      <div class="col-md-6">
        <ProductsItem
          v-for="(product, index) in isIncluded.slice(0, Math.ceil(isIncluded.length/2))"
          :key="index"
          :product="product"
        ></ProductsItem>
      </div>
      <div class="col-md-6">
        <ProductsItem
          v-for="product in isIncluded.slice(Math.ceil(isIncluded.length/2), isIncluded.length)"
          :key="product.id"
          :product="product"
        ></ProductsItem>
      </div>
    </div>
  </div>
</template> 

<script>
import { products } from "../../db.js";
import ProductsItem from "./ProductsItem";

export default {
  props: {
    categoryId: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      products: products,
    };
  },
  components: {
    ProductsItem
  },
  computed: {
    isIncluded() {
      return this.products.filter(product => {
        return product.productId.includes(this.categoryId)
      })
    }
  }
};
</script>

<style lang="scss">
.categories {
  margin: 10px;
  padding: 16px;
  border: 1px solid rgb(66, 203, 245);
  border-radius: 13px;
  cursor: pointer;

  &:hover {
    background: rgba(63, 191, 178, 0.15);
  }

  &__header {
    display: inline;
    font-size: 14px;
    margin-right: 6px;
  }

  &__amount {
    display: inline;
    font-size: 12px;
    color: grey;
  }
}
</style>