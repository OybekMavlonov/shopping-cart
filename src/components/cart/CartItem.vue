<template>
  <div class="cartItem">
    <div class="left">
      <p class="number">{{cartIndex+1}}</p>
      <div class="item-info">
        <div class="name">{{cartItem.name}}</div>
        <button class="delete" @click="deleteFromCart(cartItem.id)">
          <img src="../../assets/delete.png" alt />
        </button>
        <div class="price">{{cartItem.price}} So'm</div>
      </div>
    </div>
    <div class="right">
      <div class="total-sum">{{totalAmount()}} Сум</div>
      <button class="minus" @click="reduceAmount()">-</button>
      <button class="amount">{{cartItem.quantity}}</button>
      <button class="plus" @click="cartItem.quantity++">+</button>
    </div>
  </div>
</template>

<script>
import EventBus from "../../EventBus";

export default {
  data() {
    return {
      total: this.cartItem.price
    };
  },
  props: {
    cartItem: {
      type: Object,
      required: true
    },
    cartIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    deleteFromCart(productId) {
      EventBus.$emit("delete-from-cart", productId);
    },
    reduceAmount() {
      if (this.cartItem.quantity > 1) {
        this.cartItem.quantity--;
      } else {
        this.cartItem.quantity = 1;
      }
    },
    totalAmount() {
      this.total = this.cartItem.price * this.cartItem.quantity;
      return this.total;
    }
  }
};
</script>

<style lang="scss" scoped>
.cartItem {
  display: flex;
  justify-content: space-between;
  margin: 30px 0;

  .left {
    .number {
      float: left;
      margin-right: 20px;
      font-size: 13px;
      color: grey;
    }
    .item-info {
      float: right;
      .name {
        margin-left: -15px;
        font-size: 14px;
        font-weight: 550;
      }

      .delete {
        display: inline;
        background: #fff;
        border-radius: 5px;
        outline: none;
        border: 1px solid #1111;
        padding: 2px 10px;

        img {
          width: 12px;
        }

        &:hover {
          background: rgba(238, 238, 238, 0.5);
        }
      }
      .price {
        display: inline;
        margin-left: 10px;
        font-size: 13px;
        color: grey;
      }
    }
  }

  .right {
    .total-sum {
      float: left;
      margin-right: 14px;
      font-size: 14px;
      font-weight: 550;
    }
    button {
      background: #fff;
      border: 1px solid #1111;
      outline: none;
      padding: 2px 10px;
    }
    .minus {
      border-bottom-left-radius: 5px;
      border-top-left-radius: 5px;

      &:hover {
        background: rgba(238, 238, 238, 0.5);
      }
    }
    .amount {
      padding: 2px 20px 2px 10px;
    }
    .plus {
      border-bottom-right-radius: 5px;
      border-top-right-radius: 5px;

      &:hover {
        background: rgba(238, 238, 238, 0.5);
      }
    }
  }
}
</style>