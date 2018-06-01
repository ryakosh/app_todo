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

    <app-notifier :show="notifierCtrls.show">
      {{ notifierCtrls.message }}
    </app-notifier>
  </div>
</template>

<script>
import AppBluryOverlay from './components/AppBluryOverlay/AppBluryOverlay.vue';
import AppTaskList from './components/AppTaskList/AppTaskList.vue';
import AppCirculartton from './components/AppCirculartton/AppCirculartton.vue';
import AppTaskSearcher from './components/AppTaskSearcher/AppTaskSearcher.vue';
import AppTaskEdit from './components/AppTaskEdit/AppTaskEdit.vue';
import AppNotifier from './components/AppNotifier/AppNotifier.vue';

export default {
  name: 'app',
  components: {
    AppBluryOverlay,
    AppTaskList,
    AppCirculartton,
    AppTaskSearcher,
    AppTaskEdit,
    AppNotifier,
  },
  data() {
    return {
      tasks: this.getLocalProperty('tasks') || [],
      lastUsedID: this.getLocalProperty('lastUsedID') || 0,
      unusedIDs: this.getLocalProperty('unusedIDs') || [],
      notify: this.makeNotifier(),
      overlayCtrls: {
        show: false,
        taskEdt: {
          show: false,
          task: {},
        },
        taskSrchr: { show: false },
      },
      notifierCtrls: {
        show: false,
        message: '',
      },
    };
  },
  methods: {
    showTaskEdt(taskID) {
      this.resetOverlay();
      this.overlayCtrls.show = true;
      this.overlayCtrls.taskEdt.show = true;

      this.overlayCtrls.taskEdt.task = (
        taskID !== undefined ? this.findTask(taskID) : {}
      );
    },
    resetOverlay() {
      this.overlayCtrls.show = false;
      this.overlayCtrls.taskEdt.show = false;
      this.overlayCtrls.taskSrchr.show = false;
    },
    onEdtTask(task) {
      if (!task.todo) {
        this.notify('Please enter your todo!', 1500);
        return;
      }

      if (task.id !== undefined) {
        const foundTaskIdx = this.findTaskIdx(task.id);
        Object.assign(this.tasks[foundTaskIdx], task);
        this.upLocalProp('tasks', this.tasks);
      } else {
        this.pushTask(
          this.unusedIDs.pop() || this.lastUsedID + 1,
          task.todo,
          task.note,
        );
        this.upLocalProp('unusedIDs', this.unusedIDs);
        this.upLocalProp('lastUsedID', this.lastUsedID);
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

      this.tasks[foundTaskIdx].isComplete = (
        !this.tasks[foundTaskIdx].isComplete
      );
      this.upLocalProp('tasks', this.tasks);
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
    pushTask(id, todo, note, isComplete = false) {
      this.tasks.push({
        id, todo, note, isComplete,
      });
      this.upLocalProp('tasks', this.tasks);
    },
    delTask(taskIdx) {
      this.tasks.splice(taskIdx, 1);
      this.upLocalProp('tasks', this.tasks);
    },
    upLocalProp(propName, val) {
      localStorage[propName] = JSON.stringify(val);
    },
    getLocalProperty(propName) {
      const localProp = localStorage[propName];
      return localProp ? JSON.parse(localProp) : null;
    },
    makeNotifier() {
      let lastTimeout = null;

      return (mes, dur) => {
        clearTimeout(lastTimeout);

        this.notifierCtrls.message = mes;
        this.notifierCtrls.show = true;
        lastTimeout = setTimeout(function hideNotifier() {
          this.notifierCtrls.show = false;
        }, dur);
      };
    },
  },
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
    padding: 10px;
    transition: padding, 0.25s;
  }

  .btn-search {
    float: left;
  }

  .btn-add {
    float: right;
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
    height: 90%;
    transition-property: width, height;
    transition-duration: 0.25s;
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

// Small to medium tablet.
@media screen and (min-width: 600px) {
  #app {
    .list-tasks {
      width: 80%;
      height: 80%;
    }
  }
}

// Large tablet to laptop.
@media screen and (min-width: 960px) {
  #app {
    .top {
      padding: 15px;
    }

    .list-tasks {
      width: 70%;
    }
  }
}

@media screen and (min-width: 1264px) {
  #app {
    .list-tasks {
      width: 60%;
    }
  }
}
</style>
