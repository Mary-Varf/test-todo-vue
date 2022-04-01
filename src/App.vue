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
                @change-index="changeIndex"
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
                index: 0,
                title: 'one',
                status: false,
            },                
            {
                id: 1,
                index: 1,
                title: 'two aaaacsdvsdv vdfgdfg dfvdfvdfbv vsdvsvsv sdfsdfsdf afsedfsfsdf sefsefgwg wefwefwefwe wefrw rfw svs',
                status: true,
            },                
            {
                id: 2,
                index: 2,
                title: 'three sdfsdf fsf',
                status: false,
            },            
            {
                id: 3,
                index: 3,
                title: 'four sdfsdf fsf',
                status: false,
            },            
            {
                id: 4,
                index: 4,
                title: 'five sdfsdf fsf',
                status: false,
            },            
            {
                id: 5,
                index: 5,
                title: 'six sdfsdf fsf',
                status: false,
            },            
        ]
    }
  },
  methods: {
    deleteTask(id) {
      if (this.tasks.length) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    },
    saveNewTask(task) {
      this.tasks.unshift(task);
    },
    editTask(editTask) {
      if (this.tasks.length) {
        this.tasks.map((task) => {
          if(task.id === editTask.id) {
            task.title = editTask.title;  
          }
        })
      }
    },
    changeIndex(prevIndex, newIndex) {
      if (prevIndex < newIndex) {
        this.tasks.map(task => {
          if(task.index === prevIndex) {
            task.index = newIndex;
          } else if (task.index <= newIndex && task.index > prevIndex) {
            task.index = task.index - 1;
          }
        })
      } else if (prevIndex > newIndex) {
        this.tasks.map(task => {
          if(task.index === prevIndex) {
            task.index = newIndex;
          } else if (task.index >= newIndex && task.index < prevIndex) {
            task.index = task.index + 1;
          }
        })
      }
    }
  },
  computed: {
    getId() {
      if (this.tasks.length) {
        return this.tasks[this.tasks.length - 1].id + 1;
      } else {
        return 0;
      }
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
