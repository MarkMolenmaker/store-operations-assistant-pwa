<template>
  <div class="dashboard">
      <AppLink title="Bestelling" to="/order" icon="fas fa-pen"/>
      <AppLink title="Informatie" to="/about" icon="fas fa-question-circle" last/>
  </div>
</template>

<script>
import AppLink from '@/components/AppLink'
export default {
  name: 'Dashboard',
  components: {
    AppLink
  }
}
</script>
