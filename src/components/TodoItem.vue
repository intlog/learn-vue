<template>
  <div>
    <li>{{todo.text}}</li>
    <div>{{a}}</div>
  </div>
</template>

<script>
  export default {
    name: "TodoItem",
    props: ['todo'],
    data: function () {
      return data
    }
  }
  let data = {
    a: 1,
    newTodoText: '',
    visitCount: 0,
    hideCompletedTodos: false,
    todos: [],
    error: null
  }

</script>

<style scoped>

</style>