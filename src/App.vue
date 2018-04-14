<template>
  <div id="app">
    <app-blury-overlay v-model="overlayControls.show">
      <button @click="showTaskEdit">
        Show task edit
      </button>

      <app-task-edit class="app-task" 
        v-if="overlayControls.appTaskEdit.show" slot="overlay"
        :task="overlayControls.appTaskEdit.task" />
    </app-blury-overlay>
  </div>
</template>

<script>
import AppTaskEdit from './components/AppTaskEdit/AppTaskEdit';
import AppBluryOverlay from './components/AppBluryOverlay/AppBluryOverlay';

export default {
  name: "app",
  components: {
    AppTaskEdit,
    AppBluryOverlay
  },
  data() {
    return {
      overlayControls: {
        show: false,
        appTaskEdit: {
          show: false,
          task: {}
        }
      }
    }
  },
  methods: {
    showTaskEdit() {
      this.overlayControls.show = true;
      this.overlayControls.appTaskEdit.show = true;
    }
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  background-color: #00BCD4;

  .app-task {
    position: absolute;
    top: 0;
    left: 0;
  }
}
</style>
