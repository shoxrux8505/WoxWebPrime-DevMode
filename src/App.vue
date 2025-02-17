<template>
  <NavComponent />
  <div class="main-container">
    <RouterView />
  </div>
  <FooterComponent />
</template>
<script>
import NavComponent from './components/navComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
export default {
  name: 'App',
  components: {
    NavComponent,
    FooterComponent
  }
}
import { RouterView } from 'vue-router'

</script>

<style scoped lang="scss">
.main-container {
  width: 100%;
  min-height: 90vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
