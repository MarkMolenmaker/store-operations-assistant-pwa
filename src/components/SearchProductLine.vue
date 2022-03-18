<template>
  <div class="wrapper">
    <img class="product-image" :src="img" alt="product afbeelding">
    <div class="product-details">
      <span class="product-name">{{title}}</span>
      <span class="product-sku">{{sku}}</span>
    </div>
    <a @click="$emit('addProduct', title, sku, img)" class="product-add"><i class="icon green fas fa-plus"/></a>
  </div>
</template>

<script>
export default {
  name: 'SearchProductLine',
  emits: ['addProduct'],
  props: {
    img: { type: String, required: false, default: 'https://www.coop.nl/assets/img/header/bloemkool.png' },
    title: { type: String, required: true, default: '' },
    sku: { type: String, required: true, default: '00000000' }
  }
}
</script>

<style scoped>
span { font-size: .8em; }
.wrapper {
  display: flex;
  flex-direction: row;
  height: 3em;
  width: 100%;
  background-color: var(--white-color);
  align-items: center;
}
.product-details {
  display: flex;
  width: 100%;
  flex-direction: column;
}
.product-image { margin: 0 .5em; max-height: 2.5em; }
.product-sku { color: var(--dark-gray-color); }
.product-add { margin: 0 1em; }
.icon { font-size: 1.5em; }
</style>
