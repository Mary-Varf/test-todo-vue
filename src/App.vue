<template>
  <div id="app">
    <div class="content">
        <header class="header">
            <div class="container">
                <h1 class="title header__title">Мои задачи</h1>
                <TaskInput @save-new-task="saveNewTask" />
            </div>
        </header>
        <main class="main">
            <div class="container">
              <TasksList
                v-bind:tasks="tasks"
                @delete-task="deleteTask"
                @edit-task="editTask"
                @change-index="changeIndex"
              />
            </div>
        </main>
    </div>
    <div class="bg">
      <div class="d-flex flex-column justify-content-center w-100 h-100">
        <div class="d-flex flex-column justify-content-center align-items-center">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TasksList from './components/TasksList.vue';
import TaskInput from './components/TaskInput.vue';

export default {
  name: 'App',
  components: {
    TasksList,
    TaskInput
  },
  data() {
    return {
        tasks: this.loadList()
    }
  },
  methods: {
    setTasksToStore() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    loadList() {
      const storageTasks = localStorage.getItem('tasks');
      const taskList = storageTasks ? JSON.parse(storageTasks) : [];

      return taskList;
    },
    deleteTask(id) {
      if (this.tasks.length) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    },
    saveNewTask(task) {
      this.tasks.unshift(task);
      this.setTasksToStore();
    },
    editTask(editTask) {
      if (this.tasks.length) {
        this.tasks.map((task) => {
          if(task.id === editTask.id) {
            task.title = editTask.title;  
          }
        });
        this.setTasksToStore();
      }
    },
    changeIndex(prevIndex, newIndex) {
      this.tasks.map((task) => {
        if (task.index === prevIndex && prevIndex < newIndex) {
          task.index = newIndex + 1;
        }
        if (task.index === prevIndex && prevIndex > newIndex) {
          task.index = newIndex - 1;
        }
      })
    }
  }
}
</script>

<style>
#app {
  font-family: "Ubuntu", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
