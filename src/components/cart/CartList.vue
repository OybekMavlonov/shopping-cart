<template>
  <div class="cart-list mt-3">
    <div class="cart-list__title">Cart #1</div>
    <table class="cart-list__item">
      <tbody>
        <CartItem v-for="(item, index) in cartItems" :key="index" :cartItem="item" :cartIndex="index"></CartItem>
      </tbody>
    </table>
  </div>
</template>

<script>
import CartItem from './CartItem'
export default {
  props: {
    cartItems: {
      type: Array,
      required: true
    }
  },
  components: {
    CartItem
  }
};
</script>

<style lang="scss">
.cart-list {
  background-color: #fff;
  border-radius: 8px;
  height: 320px;
  overflow-y: scroll;
  padding: 20px;

  &__title {
    font-size: 16px;
    font-weight: 550;
    margin-top: 10px;
  }
  
  &__item {
    width: 100%;
  }
}

/* width */
::-webkit-scrollbar {
  width: 5px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1; 
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: grey; 
}
</style>