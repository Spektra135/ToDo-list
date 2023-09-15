<template>
  <div>
    <div class="item" :class="{marked: product.marked}" v-for="product in products" :key="product.id" >
      <input type="checkbox"  v-model="product.marked" :value="product" @change="$emit('change', $event.target.checked)">

      {{ product.text }}
    </div>
  </div>
</template>

<script>
  export default {
    model: {
      prop: 'checked',
      event: 'change'
    },
    props: ['products', 'value', 'checked'],
  }
</script>

<style>
  .item {
    margin: 10px 0;
  }
  .marked {
    text-decoration: line-through;
  }
</style>
