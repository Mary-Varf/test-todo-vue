<template>
    <section class="done main__section">
        <h2 class="main__title title">Tasks</h2>
        <div class="items-number">{{tasks.length ? tasks.length : '0'}}</div>
        <ul class="list-reset main__list">
            <TaskCard 
                v-for="task of tasks"
                v-bind:key="task.id"
                v-bind:task="task"
                v-on:delete-task="deleteTask"
            />
        </ul>
    </section>
</template>

<script>
import TaskCard from '@/components/TaskCard';

export default {
    props: {
        tasks: {
            type: Array,
            required: true,
        }
    },
    components: {
        TaskCard
    },
    methods: {
        deleteTask(id) {
            this.$emit('delete-task', id);
        }
    }
}
</script>
<style scoped>
    .main__section {
        position: relative;
    }
    .items-number {
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        top:0;
        right: 0;
        background-color: lightgray;
    }
</style>