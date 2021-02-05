<template>
  <div
    class="categories"
    @click="getCategoryId(category.id)"
    :class="getActiveClass(category.title)"
    :activeId="category.title"
  >
    <div class="categories__header">{{category.title}}</div>
    <div class="categories__amount">{{category.amount}}</div>
  </div>
</template>

<script>
import EventBus from "../../EventBus";
export default {
  data() {
    return {
      isActive: false,
      activeItem: null
    };
  },
  props: {
    category: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  methods: {
    getCategoryId(categoryId) {
      EventBus.$emit("get-category-id", categoryId);
      // if (categoryId === this.activeId) {
      //   this.isActive = true;
      // }
    },
    getActiveClass(id) {
      if (id === this.activeId) {
        return "active";
      } else {
        return "";
      }
    }
  }
};
</script>

<style lang="scss">
.active {
  background-color: rgba(63, 191, 178, 0.15) !important;
}
.categories {
  margin: 10px 0;
  padding: 16px;
  background-color: #fff;
  border: 1px solid rgb(66, 203, 245);
  border-radius: 10px;
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