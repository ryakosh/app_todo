<template>
  <div id="app">
    <app-blury-overlay v-model="overlayControls.show">
      <div class="content">
        <button @click="overlayControls.show = true">Show overlay</button>
      </div>

      <div class="overlay" slot="overlay">
        <app-task-searcher :tasks="tasks" />
      </div>
    </app-blury-overlay>
  </div>
</template>

<script>
import AppTaskSearcher from './components/AppTaskSearcher/AppTaskSearcher';
import AppBluryOverlay from './components/AppBluryOverlay/AppBluryOverlay';

export default {
  name: "app",
  components: { AppTaskSearcher, AppBluryOverlay },
  data() {
    return {
      tasks: [
        { id: 0, todo: "First task", note: "", isComplete: false },
        { id: 1, todo: "Second task", note: "Some note", isComplete: true },
        { id: 2, todo: "Third task", note: "Some note", isComplete: true },
        { id: 3, todo: "Four task", note: "Some note", isComplete: false },
        { id: 4, todo: "Five task", note: "Some note", isComplete: false },
        { id: 5, todo: "Six task", note: "Some note", isComplete: true },
        { id: 7, todo: "Seven task", note: "Some note", isComplete: false },
        { id: 8, todo: "Seven task", note: "Some note", isComplete: false },
        { id: 9, todo: "Seven task", note: "Some note", isComplete: true },
        { id: 10, todo: "Seven task", note: "Some note", isComplete: false },
        { id: 11, todo: "Seven task", note: "Some note", isComplete: true }
      ],
      overlayControls: {
        show: false,
        taskSearcher: {
          show: true,
          tasks: this.tasks
        }
      }
    };
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  background-color: #00bcd4;
  display: flex;

  .content {
    width: 100%;
    height: 100%;
  }

  .overlay {
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
  }
}
</style>
