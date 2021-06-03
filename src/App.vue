<template>
  <div id="app">
    <div class="header">
<!-- ========================================== -->
        <div class="top-header">

            <div class="buttons-navigations">
                <input type="text" class="goods-search" v-model="searchLine" />
                <button class="search-button" type="button" @click="filterGoods">Искать</button>      
            </div>

        </div>
<!-- ========================================== -->
        <div class="bottom-header">

            <button class="cart-button" type="button" @click="toggleCartStatus">Корзина</button>

        </div>
<!-- ========================================== -->
    </div>
    
    <main>

      Товары:
      <GoodsList :goods="filteredGoods"/>
      <br />
      <div v-show="isVisibleCart" class="goods-list"></div>
      
      <br />

      Корзина:
      <div class="cart-list"></div>
       
    </main>
  </div>
</template>

// =====================================================

<script>
import GoodsList from './components/GoodsList';

const API_URL = 'https://raw.githubusercontent.com/GeekBrainsTutorial/online-store-api/master/responses';


export default {
  name: 'App',
  components: {
    GoodsList,
  },

  data: () => ({
    goods: [],
    filteredGoods: [],
    searhLine: '',
    isVisibleCart: false,
  }),
  mounted() {
    this.makeGETRequest(`${API_URL}/catalogData.json`)
  },

  methods: {
    makeGETRequest(url) {
      fetch(url)
        .then((data) => data.json())
        .then((data) => {
          this.goods = data;
          this.filteredGoods = data;
        }) 
    },
    filterGoods() {
      const regexp = new RegExp(this.searhLine, 'i');
      this.filteredGoods = this.goods.filter(good => regexp.test(good.product_name));
    },
    toggleCartStatus() {
      this.isVisibleCart = !this.isVisibleCart;
    }
  },
  watch: {
    searhLine() {
      this.filterGoods();
    }
  }
}
</script>


