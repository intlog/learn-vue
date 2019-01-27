<template>
  <div id="app">
    <CustomInput :value="message" @input="message=$event"></CustomInput>
    <div>
      <label><input v-model="message"></label>
      <label><input :value="message"
                    @input="message=$event.target.value"
      ></label>
    </div>
    <ButtonCounter title="one"></ButtonCounter>
    <ButtonCounter title="two"></ButtonCounter>
    <ButtonCounter title="three"></ButtonCounter>
    <div :style="{fontSize: postFontSize+'em'}">
      <ButtonCounter v-for="post in posts" :key="post.id"
                     :title="post.text"
                     @enlarge-text="postFontSize+=$event"
      ></ButtonCounter>
    </div>
    <div>
      <p>message is : {{message}}</p>
      <label><input placeholder="edit me" v-model="message"></label>
      <textarea v-model="message" placeholder="add multipple lines"></textarea>
      <input type="checkbox" id="checkbox" v-model="checked">
      <label for="checkbox">{{checked}}</label>
      <div>
        <input type="checkbox" id="jack" value="jack" v-model="checkedNames">
        <label for="jack">jack</label>
        <input type="checkbox" id="john" value="john" v-model="checkedNames">
        <label for="john">john</label>
        <input type="checkbox" id="mike" value="mike" v-model="checkedNames">
        <label for="mike">mike</label>
        <br><span>checked names: {{checkedNames}}</span>
      </div>
      <div>
        <input type="radio" id="one" value="one" v-model="picked">
        <label for="one">one</label><br>
        <input type="radio" id="two" value="two" v-model="picked">
        <label for="two">two</label><br>
        <span>Picked: {{picked}}</span>
      </div>
      <div>
        <label><select v-model="selected">
          <option value="" disabled>choose</option>
          <option>A</option>
          <option>B</option>
          <option>C</option>
        </select></label>
        <span>selected: {{selected}}</span>
      </div>
      <div>
        <label><select v-model="selected2" multiple style="width: 50px">
          <option>A</option>
          <option>B</option>
          <option>C</option>
        </select></label>
        <span>selected {{selected2}}</span>
      </div>
      <div>
        <label><select v-model="selected3">
          <option v-for="(option,index) in options" :key="index"
                  :value="option.value"
          >{{option.text}}
          </option>
        </select></label>
        <span>selected:{{selected3}}</span>
      </div>
      <div>
        <label><input type="checkbox" v-model="toggle"
                      true-value="yes"
                      false-value="no"
        ></label>
        <span>toggele: {{toggle}}</span>
      </div>
      <div>
        <label><input v-model.lazy="message"></label>
        <span>message:{{message}}</span>
      </div>
      <div>
        <label><input type="number" v-model.number="age"></label>
        <span>type:{{typeof age}} age:{{age}}</span>
      </div>
      <div>
        <label><input v-model.trim="message"></label>
        <span>no space at begin and end:{{message}}</span>
      </div>
    </div>
    <div>
      <p>The button above has been clicked {{ counter }} times.</p>
      <button @click="counter+=1">add 1</button>
      <button @click="greet">greet</button>
      <button @click="say('hi')">say hi</button>
      <button @click="say('what')">say what</button>
      <button @click="warn('form cannot be subitted',$event)">submit</button>
    </div>
    <div>
      <form @submit.prevent="addNewItem">
        <label for="newItem">add a item</label>
        <input id="newItem" v-model="newItemText" placeholder="eg.feed">
        <button>add</button>
      </form>
      <ul>
        <li is="Item"
            v-for="(item,index) in items2"
            :key="item.id"
            :title="item.title"
            @remove="items2.splice(index,1)"
        ></li>
      </ul>
    </div>
    <!--<div><ul>
      <li v-for="(list,index) in lists" :key="index" v-if="list.isComplete">{{list.msg}}</li>
    </ul></div>-->
    <div>
      <ul>
        <li v-for="n in evenNumbers" :key="n">{{n}}</li>
      </ul>
      <ul>
        <li v-for="n in even(numbers)" :key="n">{{n}}</li>
      </ul>
      <span v-for="n in 10" :key="n">{{n}}</span>
      <ul>
        <template v-for="(item,index) in items">
          <li :key="index">{{item.message}}</li>
          <li class="divider" role="presentation" :key="index+2">{{index}}</li>
        </template>
      </ul>
    </div>
    <div>
      <p>{{items[0].message}}</p>
      <button @click="changeItem">change item</button>
      <button @click="changeItem2">change item</button>
      <button @click="changeItem3">change item</button>
      <button @click="changeItem4">change item</button>
      <p>{{userobj.age}}---{{userobj.color}}</p>
      <button @click="setAge">set age</button>
      <button @click="setAge2">set age</button>
      <button @click="setAttr">set attr</button>
      <button @click="setAttr2">set attr</button>
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
  import TodoItem from './components/TodoItem.vue'
  import Item from './components/Item.vue'
  import ButtonCounter from './components/ButtonCounter.vue'
  import CustomInput from './components/CustomInput.vue'
  import Vue from 'vue'

  export default {
    name: 'app',
    components: {
      HelloWorld,
      TodoItem,
      Item,
      ButtonCounter,
      CustomInput,
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
        userobj: {
          name: 'anika'
        },
        numbers: [1, 2, 3, 4, 5],
        lists: [
          {msg: 'one ', isComplete: true},
          {msg: 'twe ', isComplete: false},
          {msg: 'three ', isComplete: true}
        ],
        newItemText: '',
        items2: [
          {id: 1, title: 'Do the dishes',},
          {id: 2, title: 'Take out the trash',},
          {id: 3, title: 'Mow the lawn'}
        ],
        nextItemId: 4,
        counter: 0,
        checked: true,
        checkedNames: [],
        picked: '',
        selected: '',
        selected2: [],
        selected3: 'A',
        options: [
          {text: 'one', value: 'A'},
          {text: 'two', value: 'B'},
          {text: 'three', value: 'C'},
        ],
        toggle: '',
        age: 0,
        postFontSize: 1,
        posts: [
          {id: 1, text: 'text 1'},
          {id: 2, text: 'text 2'},
          {id: 3, text: 'text 3'},
        ]
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
      },
      evenNumbers: function () {
        return this.numbers.filter(function (number) {
          return number % 2 === 0
        })
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
      setAge: function () {
        Vue.set(this.userobj, 'age', 27)
      },
      setAge2: function () {
        this.$set(this.userobj, 'age', 30)
      },
      setAttr: function () {
        //do not
        Object.assign(this.userobj, {favoriteColor: 'vue green', color: 'blue'})
      },
      setAttr2: function () {
        this.userobj = Object.assign({}, this.userobj, {favoriteColor: 'vue green', color: 'blue'})
      },
      even: function (numbers) {
        return numbers.filter(function (number) {
          return number % 2 === 0
        })
      },
      addNewItem: function () {
        this.items2.push({
          id: this.nextItemId++,
          title: this.newItemText
        });
        this.newItemText = ''
      },
      greet: function (event) {
        alert('hello ' + this.message + '!');
        if (event) {
          alert(event.target.tagName)
        }
      },
      say: function (message) {
        alert(message)
      },
      warn: function (message, event) {
        if (event) {
          event.preventDefault()
        }
        alert(message)
      }
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
