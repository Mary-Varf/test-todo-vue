<template>
    <section class="done main__section">
        <h2 class="main__title title">Tasks</h2>
        <ul class="list-reset main__list">
            <TaskCard 
                v-for="task of sortedTaskList"
                v-bind:key="task.id"
                v-bind:task="task"
                v-bind:currentPosition="task.index"
                v-on:delete-task="deleteTask"
                v-on:edit-task="editTask"
                v-on:change-index="changeIndex"
            />
        </ul>
        <div class="result">
            <TasksNumber v-bind:title="doneTitle" v-bind:itemsNumber="doneTasksNumber" />
            <TasksNumber v-bind:title="toDoTitle" v-bind:itemsNumber="toDoTasksNumber" />
        </div>
    </section>
</template>

<script>
import TaskCard from '@/components/TaskCard';
import TasksNumber from '@/components/TasksNumber';

export default {
    data() {
        return {
            doneTitle: 'done tasks',
            toDoTitle: 'in progress tasks',
        }
    },
    props: {
        tasks: {
            type: Array,
            required: true,
        }
    },
    components: {
        TaskCard,
        TasksNumber
    },
    methods: {
        deleteTask(id) {
            this.$emit('delete-task', id);
        },
        editTask(id) {
            this.$emit('edit-task', id);
        },
        changeIndex(prevIndex, newIndex) {
            this.$emit('change-index', prevIndex, newIndex);
        },
    },
    computed: {
        doneTasksNumber() {
            return this.tasks.filter(task => task.status).length;
        },
        toDoTasksNumber() {
            return this.tasks.filter(task => !task.status).length;
        },
        sortedTaskList() {
            return this.tasks.sort((a, b) => a.index - b.index);
        }
    }
}
</script>
<style scoped>
    .main__section {
        position: relative;
    }
    .main__list {
        margin-bottom: 50px;
    }
    .result {
        display: flex;
        justify-content: space-between;
    }
    .main__title {
        margin: 50px 0;
    }
</style>