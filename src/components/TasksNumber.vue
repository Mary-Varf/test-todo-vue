<template>
  <div class="items-number">
    <h4>{{ `${title}: ${itemsNumber}`}}</h4>
  </div>
</template>

<script>


export default {
  props: {
    itemsNumber: {
      type: Number,
      required: true,
    },
    title: {
      type: String,
      required: true,
    }
  }
}
</script>

<style scoped>
  .items-number {
    border-radius: 20px;
    min-width:40%;
    padding: 10px 25px;
    background-color: white;
    box-shadow: 0 0 20px 5px rgba(0, 0, 0, 0.21);
  }
  
  .items-number:not(:last-child) {
    margin-right: 10px;
  }
</style>