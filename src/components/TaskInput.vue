<template>
    <form @submit.prevent="onSubmit" class="header__form">
        <input type="text" class="input header__input" v-model="title" />
        <button type="submit" class="header__btn btn btn-reset">Add new task</button>
    </form>
</template>

<script>

export default {
    props: {
        id: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTask = {
                    id: this.id,
                    index: this.id,
                    title: this.title,
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