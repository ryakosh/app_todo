<template>
  <div id="app">
    <app-text-edit class="btn" placeholder="What are you up to?" />
  </div>
</template>

<script>
import AppTextEdit from './components/AppTextEdit/AppTextEdit';

export default {
  name: "app",
  components: {
    AppTextEdit
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

  .btn {
    width: 100%;
  }
}
</style>
