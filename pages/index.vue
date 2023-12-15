<template>
  <div class="main">
    <Header :content="content"/>
    <div class="main_container">
      <Menu :products="products" @activeCat="filterCat($event)"/>
      <catalogList :products="content" :intersected="intersected"/>
    </div>
  </div>
</template>

<script>
import CatalogList from "@/components/catalogList.vue";
import Menu from "@/components/Menu.vue";
import Header from "@/components/Header.vue";

export default {
  name: 'IndexPage',
  components: {Header, Menu, CatalogList},
  data() {
    return {
      content: [],
    }
  },
  async asyncData({$axios}) {
    const products = await $axios.$get(`https://fakestoreapi.com/products`)

    return {products}
  },
  methods: {
    filterCat(active) {
      if (!Array.isArray(active)) {
        this.content = this.products.filter((el) => active === el?.category)
      } else if (Array.isArray(active)) {
        this.content = this.products
      }
    },
    async intersected() {
      !this.content.length ? this.content : this.content = [...this.content, ...this.content]
      this.limit += 5;
    }
  },
}
</script>
<style lang="scss">
.main {
  display: flex;
  flex-direction: column;
}

.main_container {
  display: flex;
  height: 100%;
  justify-content: space-between;
}

</style>
