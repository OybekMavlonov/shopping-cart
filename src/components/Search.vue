<template>
  <input class="mt-3 mb-4" type="text" v-model="search" />
</template>

<script>
import EventBus from '../EventBus';

export default {
  data() {
    return {
      search: ""
    };
  },
  props: {
    categories: {
      type: Array,
      required: true
    }
  },
  computed: {
    filteredCategories() {
      return this.categories.filter(category => {
        return category.title.toLowerCase().match(this.search.toLowerCase());
        
      });
    }
  },
  methods: {
    sendFilteredCategories() {
      EventBus.$emit("send-filtered-categories",  this.filteredCategories );
    }
  }
};
</script>
