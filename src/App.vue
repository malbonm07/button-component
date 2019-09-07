<template>
  <div id="app">
    <app-button rounded>
      Button Text
    </app-button>
  </div>
</template>

<script>

import AppButton from "@/components/App-Button.vue"
export default {
  name: 'app',
  components: {
    AppButton
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #333;
  min-height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
