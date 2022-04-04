<template>
  <form @submit.prevent="onSubmit" class="header__form">
    <input type="text" class="input header__input" v-model="title" placeholder='Новое задание'/>
    <button type="submit" class="header__btn btn btn-reset">Добавить задание</button>
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
          index: Date.now(),
          title: this.title,
          status: false,
        }

        this.$emit('save-new-task', newTask);
        this.title = '';
      }
    }
  }
}
</script>

<style scoped>

</style>