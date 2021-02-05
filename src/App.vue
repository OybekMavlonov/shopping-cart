<template>
  <div id="app">
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-7">
          <div class="search-box">
            <input class="search mt-4 mb-2" type="text" v-model="search" />
            <img src="./assets/magnifying-glass.svg" alt />
          </div>
          <div class="row">
            <Categories :filteredCategories="filteredCategories"></Categories>
            <Products :categoryId="categoryId"></Products>
          </div>
        </div>
        <div class="col-md-5 payment-side">
          <CartList :cartItems="cartItems"></CartList>
          <TotalAmount :cartItems="cartItems"></TotalAmount>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import Search from "./components/Search.vue";
import Categories from "./components/products/Categories.vue";
import Products from "./components/products/Products";
import CartList from "./components/cart/CartList";
import TotalAmount from "./components/cart/TotalAmount";
import { categories } from "./db.js";

import EventBus from "./EventBus";

export default {
  name: "App",
  data() {
    return {
      categories: categories,
      categoryId: NaN,
      cartItems: [],
      search: "",
    };
  },
  components: {
    // Search,
    Categories,
    Products,
    CartList,
    TotalAmount
  },
  created() {
    EventBus.$on("get-category-id", categoryId =>
      this.getCategoryId(categoryId)
    );
    EventBus.$on("add-to-cart", product => this.addToCart(product));
    EventBus.$on("delete-from-cart", productId =>
      this.deleteFromCart(productId)
    );
    EventBus.$on("send-filtered-categories", categoryItem =>
      this.searchedCategories(categoryItem)
    );
  },
  computed: {
    filteredCategories() {
      return this.categories.filter(category => {
        return category.title.toLowerCase().match(this.search.toLowerCase());
      });
    }
  },
  methods: {
    getCategoryId(categoryId) {
      this.categoryId = categoryId;
    },
    addToCart(product) {
      if (!this.cartItems.includes(product)) {
        this.cartItems.push(product);
      }
    },
    deleteFromCart(productId) {
      const index = this.cartItems.findIndex(item => item.id === productId);
      this.cartItems.splice(index, 1);
      console.log(productId);
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: rgb(245, 247, 250);
  color: #2c3e50;
}
.search-box {
  position: relative;
  .search {
    width: 99%;
    margin-left: 8px;
    border-radius: 8px;
    padding: 10px;
    padding-left: 43px;
    font-size: 15px;
    border: none;
    &:focus {
      outline: none;
    }
  }
  img {
    position: absolute;
    top: 40px;
    left: 30px;
  }
}
.payment-side {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100vh;
}
</style>
