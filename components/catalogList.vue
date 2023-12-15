<template>
  <div class="catalog_items">
    <div class="search">
      <div class="custom_input_container">
        <customInput v-model="requestText"/>
      </div>
      <div class="btn">
        <vButton :text="flag ? asc : desc" @click="sortList"/>
      </div>
      <div class="btn">
        <vButton :text="sortText" @click="sortListTitle"/>
      </div>
    </div>
    <div class="item_list">
      <div class="catalog_item" v-for="product in filterByTitle" :key="product?.id">
        <div class="catalog_item__img">
          <img :src="product?.image" :alt="product?.image">
        </div>
        <div class="catalog_item__text">
          <div class="catalog_item__text__name">{{ product?.title }}</div>
          <div class="catalog_item__text__price">{{ product?.price }}</div>
        </div>
      </div>
    </div>
    <h1 class="not_found_items" v-if="products.length === 0">Выбери категорию</h1>
    <Observer @intersect="intersected"/>
  </div>
</template>

<script>
import CustomInput from "@/components/customInput.vue";
import VButton from "@/components/vButton.vue";
import Observer from "@/components/Observer.vue";

export default {
  name: 'catalogList',
  components: {Observer, VButton, CustomInput},
  data() {
    return {
      searchBtn: 'Search',
      requestText: '',
      sortPrice: 'sort by price',
      sortText: 'sort by title',
      currentSort: 'price',
      flag: true,
      asc: 'asc',
      desc: 'desc'
    }
  },
  props: {
    products: {
      type: Array,
      default: () => []
    },
    intersected: {
      type: Function,
    },
  },
  computed: {
    filterByTitle() {
      return this.products.filter(item => item?.title.indexOf(this.requestText) !== -1)
    },
  },
  methods: {
    sortList() {
      let predicates = {
        'asc': function (a, b) {
          return (a?.price > b?.price) - (b?.price > a?.price)
        }
        , 'desc': function (a, b) {
          return (a?.price < b?.price) - (b?.price < a?.price)
        }
      }
      this.flag = !this.flag
      this.products.sort(predicates[this.flag ? 'asc' : 'desc'])
    },
    sortListTitle() {
      this.products.sort(function (a, b) {
        const firtWordA = a.title.split(' ').slice(0, 1).join('')
        const firtWordB = b.title.split(' ').slice(0, 1).join('')
        if (firtWordA < firtWordB) {
          return -1;
        }
        if (firtWordA > firtWordB) {
          return 1;
        }
        return 0;
      })
    }
  }

}
</script>

<style lang="scss" scoped>
.catalog_items {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 85%;
  padding-top: 7px;
}

.item_list {
  display: flex;
  flex-wrap: wrap;
  gap: 50px;
  justify-content: flex-start;
  padding: 25px 50px;
}

.catalog_item {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  gap: 15px;
  width: 250px;
  height: 450px;
  border: 1px solid black;

  &__img {
    align-self: center;
    width: 200px;
    height: 300px;

    & img {
      width: 100%;
      height: 100%;
    }
  }

  &__text {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 5px;
    font-size: 12px;
  }
}

.not_found_items {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  color: #2A3C93FF;
}

.search {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 25px 50px;
}

.custom_input_container {
  display: flex;
  align-items: center;
  width: 250px;
  height: 50px;
}

.btn {
  width: 100px;
  height: 32px;
}

.search {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 25px 50px;
}


</style>
