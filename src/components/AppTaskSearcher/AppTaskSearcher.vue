<template>
  <div class="ats-container">
    <div class="ats-top">
      <app-edit-text class="ats-input-search" type="search" autofocus
        v-model="searchQuery" placeholder="Search your todos..." />
    </div>

    <div class="ats-bottom">
      <app-task-list class="ats-list-tasks" :tasks="foundTasks"
        @on-task-invert="$emit('on-task-invert', $event)"
        @on-task-delete="$emit('on-task-delete', $event)"
        @on-task-edit="$emit('on-task-edit', $event)" >

        <div class="ats-indicator-not-found" slot="indicator">
          <img src="./assets/indicator-not-found.svg"
            alt="Not found indicator" />

          <span>Nothing found!</span>
        </div>
      </app-task-list>
    </div>
  </div>
</template>

<script>
import AppTaskList from '../AppTaskList/AppTaskList.vue';
import AppEditText from '../AppTextEdit/AppTextEdit.vue';

export default {
  name: 'AppTaskSearcher',
  components: {
    AppTaskList,
    AppEditText,
  },
  data() {
    return {
      searchQuery: '',
    };
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  computed: {
    foundTasks() {
      return this.tasks.filter((task) => {
        const todoLower = String(task.todo).toLowerCase();
        const noteLower = String(task.note).toLowerCase();
        const sqLower = String(this.searchQuery).toLowerCase();

        if ((todoLower.includes(sqLower)
          || noteLower.includes(sqLower))
          && sqLower) {
          return true;
        }

        return false;
      });
    },
  },

};
</script>

<style lang="scss" scoped>
.ats-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  padding: 10px 10px 0 10px;

  .ats-top {
    width: 100%;
  }

    .ats-input-search {
      width: 100%;
    }

  .ats-bottom {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: flex-end;
  }

    .ats-list-tasks {
      width: 95%;
      height: 90%;
    }

      .ats-indicator-not-found {
        width: 130px;
        width: 130px;
        text-align: center;

        img {
          margin-bottom: 20px;
        }
      }
}
</style>
