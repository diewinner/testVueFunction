<template>
  <div class="menu">
    <h2>Catalog</h2>
    <div class="menu_item" @click="checkCategory(category)" v-for="category in categories">{{ category }}</div>
    <div class="menu_item" @click="checkCategory(categories)">all</div>
  </div>
</template>

<script>
export default {
  name:'Menu',
  data() {
    return {
      activeCategory:null
    }
  },
  methods: {
    checkCategory(category) {
      this.activeCategory = category
      this.$emit('activeCat',this.activeCategory)
    },
  },
  computed: {
    categories() {
      const category = [];
      this.products.forEach(el => {
        category.push(el?.category)
      })
      const setCategories = new Set(category)
      return [...setCategories]
    }
  },
  props: {
    products: {
      type: Array,
      default: () => []
    },

  }
}
</script>

<style lang="scss" scoped>
.menu {
  display: flex;
  flex-direction: column;
  gap: 25px;
  font-size: 16px;
  box-shadow: 5px 0 5px -5px rgba(0, 0, 0, 0.6);
  width: 250px;
  padding: 50px 15px;
}

.menu_item {
  font-size: 20px;
  cursor: pointer;
  transition: all .3s linear;
  &:hover {
    color: #2A3C93FF;
    transform: scale(.95);
  }
}
</style>
