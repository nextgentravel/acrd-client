<template>
  <div id="app">
    <PrototypeBanner/>
    <div class="container">
      <Calculator msg="Accommodation and Car Rental Directory"/>
    </div>
  </div>
</template>

<script>
import PrototypeBanner from './components/PrototypeBanner.vue'
import Calculator from './components/Calculator.vue'
import Vue from 'vue'
import Autocomplete from '@trevoreyre/autocomplete-vue'
import '@trevoreyre/autocomplete-vue/dist/style.css'

Vue.use(Autocomplete)

export default {
  name: 'app',
  components: {
    Calculator,
    PrototypeBanner,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
