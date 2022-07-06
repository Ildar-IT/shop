<template>
  <div class="home">
    <filter-items @selectID="selectID"/>
    <add-product-form @submit="submit"/>
      <transition-group name="list" tag="p" class="home__items-list" >
          <product class="list-item" v-for="item in items" :key="item.id" :item="item" @delete="deleteItemID"/>
      </transition-group>
  </div>
</template>

<script>
import FilterItems from '@/components/filter-items'
import AddProductForm from '@/components/add-product-form'
import Product from '@/views/home/product'
export default {
  name: 'home',
  components: {
    AddProductForm,
    Product,
    FilterItems
  },
  data() {
    return {
      filter: '1',
      products: null,
    }
  },
  mounted() {
    this.products = JSON.parse(localStorage.getItem("products")) || [
      {id:'1',name:'Товар №1', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:1000, url: require('../assets/item.jpg')},
      {id:'2',name:'Товар №2', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:200000, url: require('../assets/item.jpg')},
      {id:'3',name:'Товар №3', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:1000000, url:require('@/assets/item.jpg')},
      {id:'4',name:'Товар №4', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:10000, url:require('@/assets/item.jpg')},
      {id:'5',name:'Товар №5', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:30000, url:require('@/assets/item.jpg')},
      {id:'6',name:'Товар №6', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:100000, url:require('@/assets/item.jpg')},
      {id:'7',name:'Товар №7', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:2000000, url:require('@/assets/item.jpg')},
      {id:'8',name:'Товар №8', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:50000, url:require('@/assets/item.jpg')},
      {id:'9',name:'Товар №9', description: 'Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк', price:40000, url:require('@/assets/item.jpg')},
    ];
  },
  watch: {
    products: {
      handler(newValue) {
        localStorage.setItem('products', JSON.stringify(newValue))
      },
      deep:true,
    }
  },
  computed: {
    items() {
      let items = this.products;

      if (this.filter === '2') {
        return items.sort(this.compareName);
      }
      if (this.filter === '3') {
        return items.sort(this.comparePriceIncrease);
      }
      if (this.filter === '4') {
        return items.sort(this.comparePriceIncrease).reverse();
      }
      return items;
    }
  },
  methods: {
    submit(item) {
      const obj = {
        id: this.generateID(),
        name: item.name,
        description: item.description,
        price: +item.price.replace(/\s/g, ""),
        url: item.url,
      }
      this.products.unshift(obj);
    },
    selectID(id) {
      this.filter = id;
    },
    deleteItemID(id) {
      this.products = this.products.filter(el => el.id !== id);
    },
    compareName(a, b) {
      if (a.name < b.name)
        return -1;
      if (a.name > b.name)
        return 1;
      return 0;
    },
    comparePriceIncrease(a, b) {
      if (a.price < b.price)
        return -1;
      if (a.price > b.price)
        return 1;
      return 0;
    },
    generateID() {
      let maxID = 0;
      this.products.map(el => {
        if(el.id > maxID) maxID = el.id;
      })
      return +maxID + 1
    }
  }
}
</script>

<style lang="scss">

.home {
  position: relative;
  box-sizing: border-box;
  display: flex;

  background: $bg;
  width: 100%;
  height: 100vh;
  padding: 83px  12px 0 ;

  @include up($sm) {
    padding: 83px  32px 0 ;
  }

  &__items-list {
    &::-webkit-scrollbar {
      width: 0;
    }
    overflow: auto;
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    margin-top: 0;

    @include up($md) {
      margin-left: 16px;
    }
  }

  .list-item {
    display: inline-block;

  }
  .list-enter-active, .list-leave-active {
    transition: all 1s;
  }
  .list-enter, .list-leave-to /* .list-leave-active до версии 2.1.8 */ {
    opacity: 0;
    transform: translateY(30px);
  }
}
</style>
