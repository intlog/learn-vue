<template>
  <div>
    <label><input :value="value"
                  @input="$emit('input',$event.target.value)"
    ></label>
  </div>
</template>

<script>
  export default {
    name: "CustomInput",
    props: ['value']
  }
</script>

<style scoped>

</style>