<template>
  <div class="ats-container">
    <div class="top">
      <app-edit-text class="input-search" type="search"
        v-model="searchQuery" placeholder="Search your todos..." />
    </div>

    <div class="bottom">
      <app-task-list class="list-tasks" :tasks="foundTasks" 
        @on-task-invert="$emit('on-task-invert', $event)"
        @on-task-delete="$emit('on-task-delete', $event)"
        @on-task-edit="$emit('on-task-edit', $event)" >

        <div class="indicator-not-found" slot="indicator">
          <img src="./assets/indicator-not-found.svg" 
            alt="Not found indicator" />

          <span>Nothing found!</span>
        </div>
      </app-task-list>
    </div>
  </div>
</template>

<script>
import AppTaskList from '../AppTaskList/AppTaskList';
import AppEditText from '../AppTextEdit/AppTextEdit';

export default {
  name: 'AppTaskSearcher',
  components: {
    AppTaskList,
    AppEditText
  },
  data() {
    return {
      searchQuery: ''
    }
  },
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  computed: {
    foundTasks: function() {
     return this.tasks.filter((task) => {
       const todoLower = task.todo.toLowerCase();
       const noteLower = task.note.toLowerCase()
       const sqLower = this.searchQuery.toLowerCase();

       if ((todoLower.includes(sqLower) || 
        noteLower.includes(sqLower)) && 
        sqLower) {
          return true;
        }
     }) 
    }
  },

}
</script>

<style lang="scss" scoped>
.ats-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  padding: 10px 10px 0 10px;

  .top {
    width: 100%;
  }

    .input-search {
      width: 100%;
    }

  .bottom {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: flex-end;
  }

    .list-tasks {
      width: 95%;
      height: 95%;
    }

      .indicator-not-found {
        width: 150px;
        width: 150px;
        text-align: center;

        img {
          margin-bottom: 20px;
        }
      }
}
</style>
