<template>
  <div id="app">
    <div>{{message}}</div>
    <div><span v-bind:title="message1">wait for few minutes to look for information</span></div>
    <div><p v-if="seen">you can see me</p></div>
    <div><ol><li v-for="todo in todos" v-bind:key="todo.id">{{todo.text}}</li></ol></div>
    <div><p>{{message2}}</p><button v-on:click="reverseMessage">reverse</button></div>
    <div><p>{{message}}</p><label><input v-model="message"></label></div>
    <img alt="Vue logo" src="./assets/logo.png">
    <ol><TodoItem
            v-for="item in groceryList"
            v-bind:todo="item"
            v-bind:key="item.id">
    </TodoItem></ol>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TodoItem from './components/TodoItem'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TodoItem
  },
  data: function () {
    return {
      message: 'hello vue!',
      message1: 'loading on ' + new Date().toLocaleString(),
      message2: 'hello vue.js!',
      seen: true,
      todos: [
        { id:1,text: '学习 JavaScript' },
        { id:2,text: '学习 Vue' },
        { id:3,text: '整个牛项目' }
      ],
      groceryList: [
        {id:0,text:'蔬菜'},
        {id:1,text:'奶酪'},
        {id:2,text:'随便其它什么人吃的东西'},
      ]
    }
  },
  methods: {
    reverseMessage: function () {
      this.message2 = this.message2.split('').reverse().join('')
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
