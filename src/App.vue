<template>
  <div id="app">
    <app-confirm-box v-model="overlay">Are you ok?</app-confirm-box>
  </div>
</template>

<script>
import AppConfirmBox from "./components/AppConfirmBox/AppConfirmBox";
export default {
  name: "app",
  components: {
    AppConfirmBox
  },
  data() {
    return {
      overlay: true
    }
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
}
</style>
