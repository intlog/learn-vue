<template>
  <div>
    <button @click="count++">clicked me {{count}} times</button>
    <span>{{title}}</span>
    <div>
      <h3>{{title}}</h3>
      <button @click="$emit('enlarge-text',0.1)">enlarge text</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "ButtonCounter",
    props: ['title'],
    data: function () {
      return {
        count: 0
      }
    }
  }
</script>

<style scoped>

</style>