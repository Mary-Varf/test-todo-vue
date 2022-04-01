<template>
    <div class="items-number">{{ `${title}: ${itemsNumber}`}}</div>
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
        },
    }
}
</script>

<style scoped>
    .items-number {
        border-radius: 20px;
        min-width:40%;
        padding: 20px 25px;
        background-color: lightblue;
        text-transform: capitalize;
    }
    .items-number:not(:last-child) {
        margin-right: 10px;
    }
</style>