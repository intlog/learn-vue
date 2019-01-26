<template>
  <div id="app">
    <div>
      <p>{{items[0].message}}</p>
      <button @click="changeItem">change item</button>
      <button @click="changeItem2">change item</button>
      <button @click="changeItem3">change item</button>
      <button @click="changeItem4">change item</button>
    </div>
    <div>
      <ul>
        <li v-for="(item, index) in items" :key="index">
          {{index}}-{{item.message}}
        </li>
      </ul>
      <ul>
        <li v-for="(item, index) of items" :key="index">
          {{index}}-{{item.message}}
        </li>
      </ul>
      <ul>
        <li v-for="(value,key,index) in obj" :key="index">
          {{index}} {{key}} {{value}}
        </li>
      </ul>
    </div>
    <div>
      <h1 v-if="ok">Yes</h1>
      <h1 v-else>No</h1>
      <template v-if="ok">
        <h1>title</h1>
        <p>paragraph 1</p>
        <p>paragraph 2</p>
      </template>
      <div v-if="type==='A'">A</div>
      <div v-else-if="type==='B'">B</div>
      <div v-else-if="type==='C'">C</div>
      <div v-else>not abc</div>
      <template v-if="loginType==='username'">
        <label>username</label>
        <input placeholder="enter your username">
      </template>
      <template v-else><label>email</label>
        <input placeholder="enter your email">
      </template>
      <template v-if="loginType==='username'">
        <label>username</label>
        <input placeholder="enter your username" key="username-input">
      </template>
      <template v-else><label>email</label>
        <input placeholder="enter your email" key="username-email">
      </template>
      <button @click="toggleLoginType">toggle login type</button>
      <h1 v-show="ok">hello</h1>
    </div>
    <div>
      <div v-bind:class="{active: isActive,text:hasError}"></div>
      <div v-bind:class="classObject"></div>
      <div v-bind:class="[activeClass, errorClass]"></div>
      <div v-bind:class="[isActive?activeClass:'',errorClass]"></div>
      <div v-bind:class="[{active: isActive},errorClass]"></div>
      <div v-bind:style="{color: activeColor,fontSize: fontSize+'px'}"></div>
      <div v-bind:style="styleObject"></div>
      <div v-bind:style="[baseStyle,overridingStyles]"></div>
      <div v-bind:style="{display: ['-webkit-box','-ms-flexbox','flex']}"></div>
    </div>
    <div>{{message}}</div>
    <div><span v-bind:title="message1">wait for few minutes to look for information</span></div>
    <div><p v-if="seen">you can see me</p></div>
    <div>
      <ol>
        <li v-for="todo in todos" v-bind:key="todo.id">{{todo.text}}</li>
      </ol>
    </div>
    <div><p>{{message2}}</p>
      <button v-on:click="reverseMessage2">reverse</button>
    </div>
    <div><p>{{message}}</p><label><input v-model="message"></label></div>
    <img alt="Vue logo" src="./assets/logo.png">
    <ol>
      <TodoItem
              v-for="item in groceryList"
              v-bind:todo="item"
              v-bind:key="item.id">
      </TodoItem>
    </ol>
    <div>
      <span>Message: {{message}}</span><br>
      <span v-once>no change: {{message}}</span>
    </div>
    <div>
      <p>Using mustaches: {{rawHtml}}</p>
      <p>Using v-html directive: <span v-html="rawHtml"></span></p>
    </div>
    <div>
      <div v-bind:id="dynamicId"></div>
      <button v-bind:disabled="isButtonDisabled"></button>
    </div>
    <div>
      <a v-bind:href="url">
        <button></button>
      </a>
      <a :href="url">
        <button></button>
      </a>
      <a v-on:click="doSomething">
        <button></button>
      </a>
      <a @click="doSomething">
        <button></button>
      </a>
    </div>
    <div>
      <p>{{message.split('').reverse().join('')}}</p>
      <p>Original message: "{{ message }}"</p>
      <p>Computed reversed message: "{{ reversedMessage }}"</p>
      <p>Reversed message: "{{ reverseMessage() }}"</p>
      <p>watch: {{fullName}}</p>
      <p>computed: {{fullNameComputed}}</p>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld.vue'
  import TodoItem from './components/TodoItem'
  import Vue from 'vue'

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
          {id: 1, text: '学习 JavaScript'},
          {id: 2, text: '学习 Vue'},
          {id: 3, text: '整个牛项目'}
        ],
        groceryList: [
          {id: 0, text: '蔬菜'},
          {id: 1, text: '奶酪'},
          {id: 2, text: '随便其它什么人吃的东西'},
        ],
        rawHtml: '<span style="color: red">This should be red</span>',
        dynamicId: 3,
        isButtonDisabled: false,
        url: 'https://bilibili.com',
        firstName: 'Foo',
        lastName: 'Bar',
        fullName: 'Foo Bar',
        isActive: true,
        hasError: true,
        error: '',
        activeClass: 'active',
        errorClass: 'text-danger',
        activeColor: 'red',
        fontSize: 30,
        styleObject: {
          color: 'red',
          fontSize: '13px'
        },
        baseStyle: {
          color: 'red',
          fontSize: '13px'
        },
        overridingStyles: {
          color: 'red',
          fontSize: '13px'
        },
        ok: true,
        type: 'A',
        loginType: 'username',
        items: [
          {message: 'Foo'},
          {message: 'Bar'}
        ],
        obj: {
          firstName: 'John',
          lastName: 'Doe',
          age: 30
        },
      }
    },
    computed: {
      reversedMessage: function () {
        return this.message.split('').reverse().join('')
      },
      fullNameComputed: function () {
        return this.firstName + ' ' + this.lastName
      },
      fullNameComputed2: {
        get: function () {
          return this.firstName + ' ' + this.lastName
        },
        set: function (newValue) {
          let names = newValue.split(' ');
          this.firstName = names[0];
          this.lastName = names[names.length - 1];
        }
      },
      classObject: function () {
        return {
          active: this.isActive && !this.error,
          text: this.error && this.error.type === 'fatal'
        }
      }
    },
    methods: {
      reverseMessage2: function () {
        this.message2 = this.message2.split('').reverse().join('');
      },
      doSomething: function () {
        alert('hahah')
      },
      reverseMessage: function () {
        return this.message.split('').reverse().join('');
      },
      toggleLoginType: function () {
        this.loginType = this.loginType === 'username' ? '' : 'username'
      },
      changeItem: function () {
        this.items[0] = {message: 'changed by change1'}
      },
      changeItem2: function () {
        this.items.splice(0, 1, {message: 'changed by change2'})
      },
      changeItem3: function () {
        this.$set(this.items, 0, {message: 'changed by change3'})
      },
      changeItem4: function () {
        Vue.set(this.items, 0, {message: 'changed by change4'})
      },
    },
    watch: {
      firstName: function (val) {
        this.fullName = val + ' ' + this.lastName
      },
      lastName: function (val) {
        this.fullName = this.firstName + ' ' + val
      }
    },
    created: function () {
      this.message = 'hello world'
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
