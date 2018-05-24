<!--
  Props: {
    tasks: "An array of individual tasks, Used for populating AppTasks"
      -> Array
  },
  Events: {
    on-task-invert: "Emitted when completion element is clicked,
      Used to invert the current state of the task" -> (id: Number),
    on-task-edit: "Emitted when the body of the task is clicked,
      Used to edit the clicked task" -> (id: Number),
    on-task-delete: "Emitted when delete button is clicked,
      Used to delete the clicked task" -> (id: Number)"
  },
  Slots: {
    indicator: "Used for showing fallback content when tasks prop is empty"
  }
-->

<template>
  <div class="atl-container">
    <ul class="atl-list-tasks" v-if="tasks.length">
      <app-task v-for="task of tasks" :task="task" :key="task.id"
        @on-task-invert="onTaskInvert"
        @on-task-edit="$emit('on-task-edit', task.id)"
        @on-task-delete="onTaskDelete" />
    </ul>

    <div class="atl-indicator-empty" v-else>
      <slot name="indicator"></slot>
    </div>

    <audio id="atl-audio-complete">
      <source src="./assets/complete.wav" type="audio/wav" />
    </audio>

    <app-confirm-box v-model="showConfirmBox" @on-settled="onSettled">
      Do you want to delete this task?
    </app-confirm-box>
  </div>
</template>

<script>
import AppTask from '../AppTask/AppTask';
import AppConfirmBox from '../AppConfirmBox/AppConfirmBox';

export default {
  name: 'AppTaskList',
  components: {AppTask, AppConfirmBox},
  props: {
    tasks: {
      type: Array,
      required: true,
      default: []
    }
  },
  data() {
    return {
      selectedTaskId: null,
      showConfirmBox: false
    }
  },
  methods: {
    onTaskInvert(taskId) {
      this.$emit('on-task-invert', taskId);
      const selectedTask = this.tasks.find(task => task.id === taskId);
      if (selectedTask.isComplete) {
        document.getElementById('atl-audio-complete').play();
      }
    },
    onTaskDelete(taskId) {
      this.showConfirmBox = true;
      this.selectedTaskId = taskId;
    },
    onSettled(isConfirmed) {
      if (isConfirmed) {
        this.$emit('on-task-delete', this.selectedTaskId);
      }
      this.selectedTaskId = null;
      this.showConfirmBox = false;
    }
  }
}
</script>

<style lang="scss" scoped>
.atl-container {
  width: 90%;
  height: 75%;
  background: white;
  border-radius: 30px 30px 0 0;
  position: relative;
  box-shadow: 0px 0px 25px 3px rgba(0, 0, 0, .5);
  overflow: hidden;
  z-index: 2;

  .atl-list-tasks {
    width: 100%;
    height: 100%;
    border-radius: inherit;
    overflow: auto;
    padding: 0;
    margin: 0;
    position: relative;
    z-index: 1;
  }

  .atl-indicator-empty {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: inherit;
  }
}
</style>
