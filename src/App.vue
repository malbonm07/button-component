<template>
  <div id="app">
    <app-button disabled category="secondary">
      Button Text Input
    </app-button>
    <button class="btn" disabled>HOLA MUNDO</button>
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
  background: #999;
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.btn {
  margin-top: 50px;
  padding: 15px;
  &:disabled {
    background-color: green;
    cursor: not-allowed;
  }
}
</style>
