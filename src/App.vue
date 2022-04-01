<template>
  <div id="app">
    <div class="content">
        <header class="header">
            <div class="container">
                <h1 class="title header__title">My Task Manager</h1>
                <TaskInput @save-new-task="saveNewTask" v-bind:id="getId" />
            </div>
        </header>
        <main class="main">
            <div class="container">
              <TasksList
                v-bind:tasks="tasks"
                @delete-task="deleteTask"
                @edit-task="editTask"
              />
            </div>
        </main>
    </div>
    <div class="yellow-bar"></div>
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
        tasks: [
            {
                id: 0,
                title: 'sdvsvs',
                status: false,
            },                
            {
                id: 1,
                title: 'aaaacsdvsdvsvs',
                status: true,
            },                
            {
                id: 2,
                title: 'sdfsdf fsf',
                status: false,
            },                
        ]
    }
  },
  methods: {
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    saveNewTask(task) {
      this.tasks.push(task);
    },
    editTask(editTask) {
      this.tasks.map((task) => {
        if(task.id === editTask.id) {
          task.title = editTask.title;  
        }
      }) 
    }
  },
  computed: {
    getId() {
      return this.tasks[this.tasks.length - 1].id + 1;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
