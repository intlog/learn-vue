<template>
  <label>{{ label }}
    <input v-bind="$attrs"
           v-bind:value="value"
           v-on:input="$emit('input', $event.target.value)"
           @="inputListeners"
    ></label>
</template>

<script>
  export default {
    name: "BaseInput",
    inheritAttrs: false,
    props: ['label', 'value','checked'],
/*    model: {
      prop: 'checked',
      event: 'change'
    },*/
    computed: {
      inputListeners: function () {
        let vm = this;
        return Object.assign({},this.$listeners,{
          input: function (event) {
            vm.$emit('input',event.target.value)
          }
        })
      }
    }
  }
</script>

<style scoped>

</style>