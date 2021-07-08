<template>
  <NewTodoField @add-todo="addTodo" />
  <TodoList :todo-items="todoItems"
            @update-todo="updateTodo"
            @delete-todo="deleteTodo" />
</template>

<script>
import NewTodoField from './components/NewTodoField.vue'
import TodoList from "./components/TodoList.vue"

export default {
  name: 'App',
  data () {
    return {
      storageKey: 'vue_memo_app',
      todoItems: []
    }
  },
  components: {
    TodoList,
    NewTodoField
  },
  methods: {
    getAllStorageData () {
      const todos = JSON.parse(localStorage.getItem(this.storageKey) || '[]')
      this.todoItems = todos
    },
    addTodo (content) {
      let nextId = Object.keys(this.todoItems)
      nextId = Math.max(...nextId) + 1
      this.todoItems[nextId] = content

      localStorage.setItem(this.storageKey, JSON.stringify(this.todoItems))
      this.getAllStorageData()
    },
    updateTodo (newTodo) {
      const [index, content] = newTodo
      this.todoItems[index] = content
      localStorage.setItem(this.storageKey, JSON.stringify(this.todoItems))
      this.getAllStorageData()
    },
    deleteTodo (index) {
      delete this.todoItems[index]
      localStorage.setItem(this.storageKey, JSON.stringify(this.todoItems))
      this.getAllStorageData()
    }
  },
  mounted() {
    this.getAllStorageData()
  }
}
</script>
