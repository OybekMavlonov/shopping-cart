<template>
  <div class="col-md-3">
    <CategoryItem
      v-for="(category,index) in filteredCategories"
      :key="index"
      :category="category"
      :index="index"
    ></CategoryItem>
  </div>
</template>

<script>
import { categories } from "../../db.js";
import CategoryItem from "./CategoryItem.vue";

export default {
  data() {
    return {
      categories: categories
    };
  },
  props: {
    filteredCategories: {
      type: Array,
      required: true
    }
  },
  components: {
    CategoryItem
  }
};
</script>

<style lang="scss">
.active {
  background-color: rgba(63, 191, 178, 0.15) !important;
}
</style>