<template>
    <form @submit.prevent="onSubmit" class="header__form">
        <input type="text" class="header__input" v-model="title" />
        <button type="submit" class="header__btn btn btn-reset">Add new task</button>
    </form>
</template>

<script>

export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTask = {
                    id: Date.now(),
                    title: this.title,
                    description: 'knn',
                    status: false,
                }

                this.$emit('save-new-task', newTask);
                this.title = '';
            }
        }
    },
}
</script>

<style scoped>

</style>