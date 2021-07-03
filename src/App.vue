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
      todoItems: this.getAllStorageData()
    }
  },
  components: {
    TodoList,
    NewTodoField
  },
  methods: {
    getAllStorageData () {
      let todoItems = {}
      for (let i = 0; i < localStorage.length; i++) {
        let key = localStorage.key(i)
        todoItems[key] = localStorage.getItem(key)
      }
      return todoItems
    },
    addTodo (content) {
      let nextId = Object.keys(this.todoItems)
      nextId = Math.max(...nextId) + 1
      localStorage.setItem(`${nextId}`, content)
      this.todoItems = this.getAllStorageData()
    },
    updateTodo (newTodo) {
      const [index, content] = newTodo
      localStorage.setItem(index, content)
      this.todoItems = this.getAllStorageData()
    },
    deleteTodo (index) {
      localStorage.removeItem(index)
      this.todoItems = this.getAllStorageData()
    }
  }
}
</script>
