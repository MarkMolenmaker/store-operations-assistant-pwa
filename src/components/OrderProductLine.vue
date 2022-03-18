<template>
  <div class="wrapper">
    <a @click="display_sku_code"><img class="product-image" :src="img" alt="product afbeelding"></a>
    <div class="product-details">
      <span class="product-name">{{title}}</span>
      <span class="product-sku">{{sku}}</span>
    </div>
    <input class="product-amount" type="number" placeholder="0" min="0" max="99" name="product-amount">
    <select class="amount-type" name="amount-type">
      <option value="st">ST</option>
      <option value="colli">Colli</option>
      <option value="tray">Tray</option>
      <option value="mp">MP</option>
    </select>
    <a class="product-remove" @click="this.$emit('removeProduct', sku)"><i class="icon red fas fa-trash-alt"/></a>
  </div>
</template>

<script>
export default {
  name: 'OrderProductLine',
  emits: ['removeProduct'],
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
.amount-type { text-align: center; margin-left: .5em;}
.product-amount { width: 1.5em; text-align: center; }
.product-image { margin: 0 .5em; max-height: 2.5em; }
.product-sku { color: var(--dark-gray-color); }
.product-remove { margin: 0 1em; }
.icon { font-size: 1em; }
</style>
