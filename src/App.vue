<template>
  <div id="app">
    <!-- <headerB /> -->
    <div class="header">
       <div class="top-header">
            <div class="buttons-navigations">

                <input v-model="searchLine" type="text" class="goods-search" />

                <button class="search-button"  type="button" @click="filterGoods">Искать</button>
                <!-- <button class="cart-button" type="button">Корзина</button> -->
                <!-- <button>3</button> -->
            </div>
        </div>
        <div class="bottom-header">
            <button class="cart-button" type="button">Корзина</button>
        </div>
      <!-- <input type="text" class="goods-search" />
      <button class="search-button" type="button">Искать</button>
      <button class="cart-button" type="button">Корзина</button> -->
    </div>
    <main>
      Товары:
      <div class="goods-list">
        <div v-for="item in filteredGoods" :key="item.id_product" class="goods-item">
          <h3>{{ item.product_name }}</h3>
          <p>{{ item.price }}</p>
          <button class="buy-button"><b>Добавить</b></button>
        </div>
      </div>
      <br />
      Корзина:
      <div class="cart-list">
        <h3>{{ item.product_name }}</h3>
          <p>{{ item.price }}</p>
      </div>
    </main>
  </div>
</template>

// =====================================================

<script>

const API_URL = 'https://raw.githubusercontent.com/GeekBrainsTutorial/online-store-api/master/responses'


export default {
  name: 'App',

  data: () => ({
    goods:  [],
    filteredGoods: [],
    basketGoods: []
  }),

  mounted() {
    this.makeGETRequest(`${API_URL}/catalogData.json`)
  },

  methods: {

    makeGETRequest(url) {
     fetch(url)
      .then( (data) => data.json() )
      .then( (data) => {
        this.goods = data;
        this.filteredGoods = data;
      })
    },
  filterGoods() {
    const regexp = new RegExp(this.searchLine, 'i');
    this.filteredGoods = this.goods.filter(good => regexp.test(good.product_name))
  }
  }
 
}
</script>


