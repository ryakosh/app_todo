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
    <div class="ate-top">
      <app-text-edit class="ate-todo" v-model="updatedTask.todo"
        placeholder="What are you up to?" />
    </div>

    <div class="ate-middle">
      <app-note-edit class="ate-note" v-model="updatedTask.note"
        placeholder="Add you're extra notes here..." />
    </div>

    <div class="ate-bottom clearfix">
      <app-circulartton class="ate-edit" bg="#009688" @click.native="editTask">
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

  .ate-top, .ate-middle {
    margin-bottom: 10px;
  }

  .ate-top {
    width: 100%;
  }

    .ate-todo {
      width: 100%;
    }

  .ate-middle {
    width: 100%;
    height: 100%;
  }

    .ate-note {
      width: 100%;
      height: 60%;
    }

  .ate-bottom {
    width: 100%;
  }

    .ate-edit {
      float: right;
    }
}
</style>
