<template>
  <div class="testing">
    <input type="text" placeholder="barcode" name="barcode" autocomplete="off" v-model="barcode">
    <span>{{barcode}}</span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      barcode: ''
    }
  }
}
</script>

<style scoped>
.testing {
  display: flex;
  flex-direction: column;
  padding: 1em;
}
input {
  height: 2em;
}
span {
  font-family: 'Libre Barcode 128', cursive;
  margin-top: 1em;
  font-size: 5em;
  text-align: start;
}
</style>
