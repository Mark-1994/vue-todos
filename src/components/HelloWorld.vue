<template>
  <div class="hello">
    <section class="todoapp">
      <header class="header">
        <h1>todos</h1>
				<input class="new-todo" placeholder="What needs to be done?" autofocus @keydown.enter="addTask">
			</header>
			<template v-if="todoList.length">
        <!-- This section should be hidden by default and shown when there are todos -->
        <section class="main">
          <input id="toggle-all" class="toggle-all" type="checkbox">
          <label for="toggle-all">Mark all as complete</label>
          <ul class="todo-list">
            <!-- These are here just to show the structure of the list items -->
            <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
            <!-- <li class="completed">
              <div class="view">
                <input class="toggle" type="checkbox" checked>
                <label>Taste JavaScript</label>
                <button class="destroy"></button>
              </div>
              <input class="edit" value="Create a TodoMVC template">
            </li> -->
            <li v-for="(item, index) in todoList" :key="item.id" :class="{completed : item.completed}">
              <div class="view">
                <input class="toggle" type="checkbox" v-model="item.completed">
                <label>{{ item.title }}</label>
                <button class="destroy" @click="deleTask(index)"></button>
              </div>
              <input class="edit" value="Rule the web">
            </li>
          </ul>
        </section>
        <!-- This footer should hidden by default and shown when there are todos -->
        <footer class="footer">
          <!-- This should be `0 items left` by default -->
          <span class="todo-count"><strong>0</strong> item left</span>
          <!-- Remove this if you don't implement routing -->
          <ul class="filters">
            <li>
              <a class="selected" href="#/">All</a>
            </li>
            <li>
              <a href="#/active">Active</a>
            </li>
            <li>
              <a href="#/completed">Completed</a>
            </li>
          </ul>
          <!-- Hidden if no completed items are left ↓ -->
          <button class="clear-completed">Clear completed</button>
        </footer>
      </template>
		</section>
		<footer class="info">
			<p>Double-click to edit a todo</p>
			<!-- Remove the below line ↓ -->
			<p>Template by <a href="http://sindresorhus.com">Sindre Sorhus</a></p>
			<!-- Change this out with your name and url ↓ -->
			<p>Created by <a href="http://todomvc.com">you</a></p>
			<p>Part of <a href="http://todomvc.com">TodoMVC</a></p>
		</footer>
  </div>
</template>

<script>
// 引入外部的样式文件
import 'todomvc-common/base.css'
import 'todomvc-app-css/index.css'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      todoList: [
        {
          id: 1,
          title: '敲代码1',
          completed: false
        },
        {
          id: 2,
          title: '敲代码2',
          completed: false
        }
      ]
    }
  },
  methods: {
    // 添加任务功能
    addTask (e) {
      // console.log(e)
      var target = e.target
      // 获取输入框中的值
      var value = target.value
      // console.log(value)
      // 把任务添加到 todolist 数组中
      var todos = this.todoList
      // 添加任务之前，检测内容是否为空
      if (!value.length) return
      todos.push({
        id: todos.length ? todos[todos.length - 1].id + 1 : 1,
        title: value,
        completed: false
      })
      // 清空文本框中的值
      target.value = ''
    },
    // 删除任务功能
    deleTask (index) {
      // console.log(index)
      this.todoList.splice(index, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
