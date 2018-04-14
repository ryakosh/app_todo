<!--
  Props: {
    task: "The task to be edited, It can be an empty object or
      an object in the form of `{todo: String, note: String}`" -> Object
  },
  Events: {
    on-edit-task: "Emitted when task is ready to be 
      edited(when edit button is clicked)" -> (Object)
  }
-->

<template>
  <div class="ate-container">
    <div class="top">
      <app-text-edit class="todo" v-model="updatedTask.todo"
        placeholder="What are you up to?" />
    </div>

    <div class="middle">
      <app-note-edit class="note" v-model="updatedTask.note"
        placeholder="Add you're extra notes here..." />
    </div>

    <div class="bottom clearfix">
      <app-circulartton class="edit" bg="#009688" @click.native="editTask">
        <img src="../../assets/images/tick-white.svg" alt="Edit button" />
      </app-circulartton>
    </div>
  </div>
</template>

<script>
import AppCirculartton from '../AppCirculartton/AppCirculartton';
import AppTextEdit from '../AppTextEdit/AppTextEdit'
import AppNoteEdit from '../AppNoteEdit/AppNoteEdit';

export default {
  name: 'AppTaskEdit',
  components: {
    AppCirculartton,
    AppTextEdit,
    AppNoteEdit
  },
  props: {
    task: {
      type: Object,
      required: false,
      default: {}
    }
  },
  data() {
    return {
      updatedTask: {todo: this.task.todo, note: this.task.note}
    };
  },
  methods: {
    editTask() {
      this.$emit('on-edit-task', {...this.task, ...this.updatedTask});
    }
  }
};
</script>

<style lang="scss" scoped>
.ate-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  padding: 10px;

  .top, .middle {
    margin-bottom: 10px;
  }

  .top {
    width: 100%;
  }

    .todo {
      width: 100%;
    }

  .middle {
    width: 100%;
    height: 100%;
  }

    .note {
      width: 100%;
      height: 60%;
    }

  .bottom {
    width: 100%;
  }

    .edit {
      float: right;
    }
}
</style>
