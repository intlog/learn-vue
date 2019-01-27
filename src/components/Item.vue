<template>
  <li>
    {{title}}
    <button @click="$emit('remove')">remove</button>
  </li>
</template>

<script>
  export default {
    name: "Item",
    props: ['title']
  }
</script>

<style scoped>

</style>