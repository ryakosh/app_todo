<template>
  <div id="app">
    <app-note-edit class="edit" placeholder="You should something in here..." />
  </div>
</template>

<script>
import AppNoteEdit from './components/AppNoteEdit/AppNoteEdit';

export default {
  name: "app",
  components: {
    AppNoteEdit
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #00BCD4;
  padding: 10px;

  .edit {
    width: 90%;
    height: 300px;
  }
}
</style>
