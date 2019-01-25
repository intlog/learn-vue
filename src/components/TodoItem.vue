<template>
    <div>
        <li>{{todo.text}}</li>
    </div>
</template>

<script>
    export default {
        name: "TodoItem",
        props: ['todo'],
    }
</script>

<style scoped>

</style>