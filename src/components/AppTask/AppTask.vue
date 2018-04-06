<!--
  Props: {
    task: "An object representing a single task" ->
      {todo: "Todo text" -> String, 
       note: "Additional note for the task" -> String,
       isComplete: "Completion state of the task" -> Boolean}
  },
  Events: {
    on-task-invert: "Emitted when completion element is clicked,
      Used to invert the current state of the task" -> (id: Number),
    on-task-edit: "Emitted when the body of the task is clicked,
      Used to edit the clicked task" -> (id: Number),
    on-task-delete: "Emitted when delete button is clicked,
      Used to delete the clicked task" -> (id: Number)
  }
-->

<template>
  <li class="at-container">
    <div class="left">
      <div :class="['completion-mark', {checked: task.isComplete}]" 
        @click="$emit('on-task-invert', task.id)">
      </div>
    </div>

    <div class="center" @click="$emit('on-task-edit', task.id)">
      <p>{{ task.todo }}</p>
    </div>

    <div class="right">
      <img class="indicator-note" v-if="task.note" 
        src="./assets/bars-black.svg" alt="Bars icon" />

      <app-circulartton @click.native="$emit('on-task-delete', task.id)"
        bg="#e53935">
        <img src="../../assets/images/x-white.svg" alt="Delete button" />
      </app-circulartton>
    </div>
  </li>
</template>

<script>
import AppCirculartton from "../AppCirculartton/AppCirculartton";

export default {
  name: "AppTask",
  components: { AppCirculartton },
  props: {
    task: {
      type: Object,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.at-container {
  width: 100%;
  height: 70px;
  display: flex;

  .left {
    height: 100%;
    display: flex;
    align-items: center;
    padding: 5px 5px 5px 0;
  }

    .completion-mark {
      width: 40px;
      height: 35px;
      border: 1px solid #4db8ad;
      border-left: none;
      border-radius: 0 20px 20px 0;
      cursor: pointer;
      position: relative;
      transition: background-color 0.25s;

      &:after {
        content: "";
        width: 10px;
        height: 5px;
        position: absolute;
        top: 50%;
        left: 50%;
        border: solid rgba(158, 158, 158, 0.5);
        border-width: 0 0 3px 3px;
        transform: rotate(-45deg);
        display: block;
        transition: border-color 0.25s;
      }
    }

    .completion-mark:hover,
    .completion-mark.checked {
      background-color: #4db8ad;

      &:after {
        border-color: white;
      }
    }

  .center {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    padding: 5px;
    cursor: pointer;
    overflow: hidden;
  }

    p {
      width: 100%;
      text-overflow: ellipsis;
      white-space: nowrap;
      overflow: hidden;
    }

  .right {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5px;
  }

    .indicator-note {
      width: 12px;
      height: 12px;
      margin-right: 5px;
    }
}
</style>
