<template>
  <div class="payment-board">
    <div class="payment-info">
      <h5>Hammasi</h5>
      <p>{{cartTotal()}} Сум</p>
    </div>
    <div class="payment-info">
      <h5>Chegirma (%)</h5>
      <!-- <p>{{discount}} %</p> -->
      <input type="number" min="0" v-model="discount"/>
    </div>
    <div class="payment-info">
      <h5>Jami to'lov</h5>
      <p>{{finalPayment()}} Сум</p>
    </div>
    <button class="payment-btn">To'lash</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      discount: 0
    };
  },
  props: {
    cartItems: {
      type: Array,
      required: true
    }
  },
  methods: {
    cartTotal() {
      return this.cartItems
        .reduce((acc, cartItem) => {
          return cartItem.quantity * cartItem.price + acc;
        }, 0)
        .toFixed(2);
    },
    finalPayment() {
      if (this.discount > 0) {
        return (
          this.cartTotal() -
          (this.discount * this.cartTotal()) / 100
        ).toFixed(2);
      } else {
        return this.cartTotal();
      }
    }
  }
};
</script>

<style lang="scss">
.payment-board {
  background-color: rgb(13, 7, 51);
  border-radius: 10px;
  padding: 20px;
  margin: 20px 0;

  .payment-info {
    display: flex;
    justify-content: space-between;
    font-weight: 550;

    h5 {
      font-size: 15px;
      color: rgb(113, 108, 145);
      font-weight: 550;
    }

    p {
      color: #fff;
      font-size: 15px;
    }
    input {
      width: 73px;
      margin-bottom: 10px;
    }
  }

  .payment-btn {
    background-color: rgb(56, 158, 6);
    color: #fff;
    padding: 10px 15px;
    border-radius: 10px;
    outline: none;
    border: none;
  }
}
</style>