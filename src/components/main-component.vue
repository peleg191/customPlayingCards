<template>
  <div>
    <div class="container">
      <card-component :ratio="ratio" :current-card="currentCard" :current-shape="shape" :current-back="back"
        :back-color="backColor"></card-component>
    </div>
    <menu-deck-component :shape="shape" :current-back="back" :back-color="backColor"
      @choose-card="currentCard = $event"></menu-deck-component>
    <dashboard-component @choose-shape="shape = $event" @choose-back="chooseBack"
      @save-preset="savePreset"></dashboard-component>
  </div>
  <!-- <input v-model="ratio" type="number"/> -->
</template>
<script>
import cardComponent from './card-component.vue';
import dashboardComponent from './dashboard-component.vue';
import MenuDeckComponent from './menu-deck-component.vue';
import storage from '../scripts/storage';
export default {
  name: 'main-component',
  components: { cardComponent, MenuDeckComponent, dashboardComponent },
  data() {
    return {
      ratio: 1.438,
      currentCard: 1,
      shape: '',
      back: '',
      backColor: ''
    }
  },
  methods: {
    chooseBack($event) {
      this.back = $event.component;
      this.backColor = $event.color;
    },
    savePreset() {
      const val = { back: this.back, backColor: this.backColor };
      storage.setItem('data', val);
    }
  },
  mounted() {
    const data = storage.getItem('data');
    this.back = data.back || '';
    this.backColor = data.backColor || '#000000';
  }

}
</script>
<style scoped>
body,
html {
  background: #222;
  height: 100%;
  display: grid;
}

.container {
  max-width: 50vw;
  margin: auto;
}
</style>