<template>
  <div id="app">
    <app-blury-overlay v-model="overlayCtrls.show">
      <div class="content">
        <div class="top clearfix">
          <app-circulartton 
            @click="showTaskSrchr" 
            class="btn-search" bg="white">
            <img src="./assets/images/loupe-gray.svg" alt="Search button" />
          </app-circulartton>

          <app-circulartton class="btn-add" 
            @click="showTaskEdt" bg="white">
            <img src="./assets/images/plus-gray.svg" alt="Add button" />
          </app-circulartton>
        </div>

        <div class="middle">
          <h1>My Do</h1>
        </div>

        <div class="bottom">
          <app-task-list class="list-tasks" :tasks="tasks"
           @on-task-edit="showTaskEdt"
           @on-task-delete="onDelTask"
           @on-task-invert="onInvertTask" >
            <div class="indicator-empty" slot="indicator">
              <img src="./assets/images/empty-box-yellow.svg" 
                alt="No tasks indicator" />

              <span>No tasks!, Click +</span>
            </div>
          </app-task-list>
        </div>

        <div class="underlay"></div>
      </div>

      <div class="overlay" slot="overlay">
        <app-task-edit class="task-edit" 
          v-show="overlayCtrls.taskEdt.show"
          :task="overlayCtrls.taskEdt.task" 
          @on-edit-task="onEdtTask" />
        
        <app-task-searcher class="task-searcher" 
          v-show="overlayCtrls.taskSrchr.show"
          :tasks="tasks"
          @on-task-edit="showTaskEdt"
          @on-task-delete="onDelTask"
          @on-task-invert="onInvertTask" />
      </div>
    </app-blury-overlay>
  </div>
</template>

<script>
import AppBluryOverlay from "./components/AppBluryOverlay/AppBluryOverlay";
import AppTaskList from "./components/AppTaskList/AppTaskList";
import AppCirculartton from "./components/AppCirculartton/AppCirculartton";
import AppTaskSearcher from "./components/AppTaskSearcher/AppTaskSearcher";
import AppTaskEdit from "./components/AppTaskEdit/AppTaskEdit";

export default {
  name: "app",
  components: {
    AppBluryOverlay,
    AppTaskList,
    AppCirculartton,
    AppTaskSearcher,
    AppTaskEdit
  },
  data() {
    return {
      tasks: [],
      lastUsedID: 0,
      unusedIDs: [],
      overlayCtrls: {
        show: false,
        taskEdt: {
          show: false,
          task: {}
        },
        taskSrchr: {
          show: false
        }
      }
    };
  },
  methods: {
    showTaskEdt(taskID) {
      this.resetOverlay();
      this.overlayCtrls.show = true;
      this.overlayCtrls.taskEdt.show = true;

      this.overlayCtrls.taskEdt.task = taskID !== undefined ?
        this.findTask(taskID) : {};
    },
    resetOverlay() {
      this.overlayCtrls.show = false;
      this.overlayCtrls.taskEdt.show = false;
      this.overlayCtrls.taskSrchr.show = false;
    },
    onEdtTask(task) {
      if (task.id !== undefined) {
        const foundTaskIdx = this.findTaskIdx(task.id);
        Object.assign(this.tasks[foundTaskIdx], task);
      } else {
        this.pushTask(this.unusedIDs.pop() || this.lastUsedID++,
          task.todo, task.note);
      }

      this.resetOverlay();
    },
    onDelTask(taskID) {
      const foundTaskIdx = this.findTaskIdx(taskID);

      this.delTask(foundTaskIdx);
      this.unusedIDs.push(taskID);
    },
    onInvertTask(taskID) {
      const foundTaskIdx = this.findTaskIdx(taskID);

      this.tasks[foundTaskIdx].isComplete = !this.tasks[foundTaskIdx]
        .isComplete;
    },
    showTaskSrchr() {
      this.resetOverlay();
      this.overlayCtrls.show = true;
      this.overlayCtrls.taskSrchr.show = true;
    },
    findTaskIdx(taskID) { 
        return this.tasks.findIndex(t => t.id === taskID);
    },
    findTask(taskID) {
      return this.tasks.find(t => t.id === taskID);
    },
    pushTask(id, todo, note, isComplete=false) {
      this.tasks.push({id, todo, note, isComplete});
    },
    delTask(taskIdx) {
      this.tasks.splice(taskIdx, 1);
    }
  }
};
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  display: flex;

  .content {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
  }

  .top {
    width: 100%;
    padding: 5px;
  }

  .btn-search {
    float: left;
  }

  .btn-add {
    float: right;
  }

  .middle {
    width: 100%;
    text-align: center;
    color: white;
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
    height: 100%;
  }

  .indicator-empty {
    width: 150px;
    height: 150px;
    text-align: center;

    img {
      margin-bottom: 20px;
    }
  }

  .underlay {
    width: 100%;
    height: 50%;
    background-color: #212121;
    position: fixed;
    top: 0;
    left: 0;
    z-index: -10;
  }

  .overlay {
    width: 100%;
    height: 100%;
  }
}
</style>
