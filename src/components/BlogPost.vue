<template>
  <div class="form-control"></div>
</template>

<script>
  export default {
    name: "BlogPost",
    // props: ['title', 'likes', 'isPublished', 'commentIds', 'author'],
    props: {
      title:String,
      likes: Number,
      isPublished: Boolean,
      commentIds: Array,
      author: Object,
      propA: Number,
      propB: [String,Number],
      propC: {
        type: String,
        required: false
      },
      propD: {
        type: Number,
        default: 100
      },
      propE: {
        type: Object,
        default: function () {
          return { message: 'hello' }
        }
      },
      propF: {
        validator: function (value) {
          return ['success', 'warning', 'danger'].indexOf(value) !== -1
        }
      }
    },
    inheritAttrs: false,
  }
</script>

<style scoped>

</style>