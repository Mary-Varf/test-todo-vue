<template>
    <li class="main__item item grid" v-bind:class="{checked: task.status}">
        <div class="item__checkbox">
            <input type="checkbox" class="custom-checkbox" v-model="task.status"/>
            <label for="happy"></label>
        </div>
        <p class="item__title">{{task.title}}</p>
        <p class="item__descr">{{task.description}}</p>
        <button class="btn btn-reset btn-delete" v-on:click="$emit('delete-task', task.id)">Delete</button>
    </li>
</template>

<script>


export default {
    props: {
        task: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style scoped>
    .checked > .item__title, .checked > .item__descr{
        text-decoration: line-through;
    }
</style>