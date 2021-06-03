<template>
  <div>
    Элитные товары:
    <div class="goods-list">
      <div v-for="item in goods" :key="item.id_product" class='goods-item'>
        <h3>{{item.product_name}}</h3>
        <p>{{item.price}}</p>
        <button>Добавить</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    goods: {
      type: Array,
      default: () => [],
    }
  }
}
</script>
