<template>
  <div class="spacer">
    <div class="block" :class="side_color"/>
    <div class="block" :class="middle_color"/>
    <div class="block" :class="side_color"/>
  </div>
</template>

<script>
export default {
  name: 'HorizontalDivider',
  props: {
    side_color: { type: String, default: 'white' },
    middle_color: { type: String, default: 'light-gray' }
  }
}
</script>

<style scoped>
  .spacer {
    display: grid;
    grid-template-columns: 1fr 18fr 1fr;
  }
  .block { height: .1em; }
</style>
