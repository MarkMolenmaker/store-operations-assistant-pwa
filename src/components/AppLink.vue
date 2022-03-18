<template>
  <router-link :to="to" class="container">
    <i class="icon" :class="icon"/>
    <span>{{title}}</span>
    <i class="icon right fas fa-angle-right"/>
  </router-link>
  <HorizontalDivider v-if="!last"/>
</template>

<script>
import HorizontalDivider from '@/components/HorizontalDivider'
export default {
  name: 'AppLink',
  components: { HorizontalDivider },
  props: {
    to: { type: String, required: true },
    icon: { type: String, required: true },
    title: { type: String, required: true },
    last: { type: Boolean, required: false, default: false }
  }
}
</script>

<style scoped>
  .container {
    display: flex;
    flex-direction: row;
    background-color: var(--white-color);
    color: var(--black-color);
    text-decoration: none;
    justify-content: start;
    align-items: center;
  }
  .container * {
    margin: .75em 0;
  }
  .icon {
    font-size: 1.3em;
    margin-left: 1em;
    margin-right: 1em;
    color: var(--orange-color);
  }
  .icon.right {
    margin-left: auto;
    color: var(--black-color);
  }
</style>
