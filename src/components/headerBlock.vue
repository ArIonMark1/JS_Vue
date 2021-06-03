<template>
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
</template>

<script>

export default {
    name: 'HeaderBlock',
    data: ({

    }),
    methods: {
        filterGoods() {
            const regexp = new RegExp(this.searhLine, 'i');
            this.filteredGoods = this.goods.filter(good => regexp.test(good.product_name));
    },
    }

 
}
</script>



