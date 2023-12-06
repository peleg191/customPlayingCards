<template>
    <main-component></main-component>
</template>
<script>
import mainComponent from './components/main-component.vue';
export default {
  components:{mainComponent}
}
</script>
<style scoped>
body, html {
  background: #222;
  height: 100%;
  display: grid;
  overflow-y:hidden;
}
</style>