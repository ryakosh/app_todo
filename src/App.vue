<template>
  <div id="app">
    <ul>
      <app-task v-for="task of tasks" :task="task" :key="task.id" />
    </ul>
  </div>
</template>

<script>
import AppTask from "./components/AppTask/AppTask";
export default {
  name: "app",
  components: {
    AppTask
  },
  data() {
    return {
      tasks: [
        {todo: 'short one', note: 'hey', isComplete: false},
        {todo: 'short one number 2', isComplete: true},
        {todo: 'short one', note: 'hey', isComplete: false},
        {todo: 'long one long one long one long one long one long one long one ', note: 'hey', isComplete: true},
      ]
    }
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column-reverse;
  justify-content: flex-start;
  align-items: center;
  background-color: rgb(33,33,33);

  ul {
    width: 95%;
    height: 80%;
    background-color: white;
    margin: 0;
    padding: 0;
    border-radius: 25px 25px 0 0;
  }
}
</style>
