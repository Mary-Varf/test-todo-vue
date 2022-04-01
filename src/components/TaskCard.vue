<template>
    <li class="main__item item grid" v-bind:class="{checked: task.status}">
        <div class="item__checkbox">
            <input type="checkbox" class="custom-checkbox" v-model="task.status"/>
            <label for="happy"></label>
        </div>
        <p v-if="!edit" class="item__title">{{task.title}}</p>
        <input ref="text" v-mode="title"  v-else class="input item__input"/>
        
        <button  class="btn btn-reset btn-edit" v-on:click="changeFunction">{{changeButtonName()}}</button>
        <button class="btn btn-reset btn-delete" v-on:click="$emit('delete-task', task.id)">Delete</button>
    </li>
</template>

<script>


export default {
    data() {
        return {
            title: this.task.title,
            edit: false,
        }
    },
    methods: {
        handleEdit() {
            this.$emit('edit-task', this.task.id);
            this.edit = !this.edit;
            console.log(this.$refs.text.focus());
        },
        handleSave() {
            if (this.title.trim()) {
                const newTask = {...this.task, title: this.title};
                this.$emit('edit-task', newTask);
                this.edit = !this.edit;
            }
        },
        changeButtonName() {
            return !this.edit ? 'Edit' : 'Save'
        },
        changeFunction() {
            return this.edit ? this.handleEdit() : this.handleSave();
        }
    },
    props: {
        task: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style scoped>
    .checked > .item__title{
        text-decoration: line-through;
    }
    .main__item {
        margin: 20px 0;
    }
    .main__item > p {
        margin:0;
    }
</style>