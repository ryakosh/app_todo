<template>
  <div id="app">
    <app-blury-overlay v-model="overlay">
      some content somecontent
      some content somecontent
      some content somecontent

      <div slot="overlay">
      some content somecontent
      some content somecontent
      </div>
    </app-blury-overlay>
  </div>
</template>

<script>
import AppBluryOverlay from "./components/AppBluryOverlay/AppBluryOverlay";
export default {
  name: "app",
  components: {
    AppBluryOverlay
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
