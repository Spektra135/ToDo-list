<template>
  <div class="container">
    <h1>Список продуктов</h1>

    <ProductsList :products="unmarkedProducts"   @change="updateProduct"></ProductsList>

    <ProductsList :products="markedProducts" @change="updateProduct"></ProductsList>

    <div class="form">
      <input :placeholder="placeholder" v-model="value" @keyup.enter="addProduct()">

      <button class="button" :type="type" @click="addProduct()">Добавить</button>
    </div>
  </div>
</template>

<script>
  import ProductsList from "@/components/ProductsList";

  export default {
    components: {ProductsList},
    data() {
      return {
        value: '',
        placeholder: 'Запишите продукт',
        type: 'button',
        products: localStorage.getItem('listProducts') ? JSON.parse(localStorage.getItem('listProducts')) : [],
      }
    },
    methods: {
      addProduct() {
        this.products.push({text: this.value, marked: false, id: this.products.length + 1});
        localStorage.setItem('listProducts', JSON.stringify(this.products))
        this.value='';
      },
      updateProduct() {
        localStorage.setItem('listProducts', JSON.stringify(this.products))
      },
    },
    computed: {
      unmarkedProducts() {
        console.log('неотмеченные');
        return this.products.filter(product => !product.marked);
      },
      markedProducts() {
        console.log('вычеркнут')
        return this.products.filter(product => product.marked);
      },
    },
  }
</script>
<style>
  .container {
    max-width: 700px;
    margin: 0 auto;
    overflow: hidden;
  }
  .form {
    margin: 20px 0;
  }
  .button {
    margin: 0 10px;
  }
</style>
