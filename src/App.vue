<template>
  <div id="app">
    <app-task-list :tasks="tasks" @on-task-invert="onTaskInvert">
      <p slot="indicator">Sorry, nothing to show</p>
    </app-task-list>
  </div>
</template>

<script>
import AppTaskList from './components/AppTaskList/AppTaskList';

export default {
  name: "app",
  components: {AppTaskList},
  data() {
    return {
      tasks: [
        {id: 0, todo: 'First task', note: '', isComplete: false},
        {id: 1, todo: 'Second task', note: 'Some note', isComplete: true},
        {id: 2, todo: 'Third task', note: 'Some note', isComplete: true},
        {id: 3, todo: 'Four task', note: 'Some note', isComplete: false},
        {id: 4, todo: 'Five task', note: 'Some note', isComplete: false},
        {id: 5, todo: 'Six task', note: 'Some note', isComplete: true},
        {id: 7, todo: 'Seven task', note: 'Some note', isComplete: false},
        {id: 8, todo: 'Seven task', note: 'Some note', isComplete: false},
        {id: 9, todo: 'Seven task', note: 'Some note', isComplete: true},
        {id: 10, todo: 'Seven task', note: 'Some note', isComplete: false},
        {id: 11, todo: 'Seven task', note: 'Some note', isComplete: true},
      ]
    }
  },
  methods: {
    onTaskInvert(taskId) {
      let found = this.tasks.find(task => task.id === taskId);
      found.isComplete = !found.isComplete;
    }
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  background-color: #00BCD4;
  display: flex;
  justify-content: center;
  align-items: flex-end;
}
</style>
