<template>
  <ul class="list-group">
    <ListItem v-for="(content, index) in todoItems"
              :index="index"
              :content="content"
              :key="index"
              @delete-todo="deleteTodo"
              @update-todo="updateTodo" />
  </ul>
</template>

<script>
import ListItem from "./ListItem.vue"

export default {
  name: 'TodoList',
  props: ['todoItems'],
  components: {
    ListItem
  },
  methods: {
    updateTodo (...newTodo) {
      this.$emit('updateTodo', newTodo)
    },
    deleteTodo (index) {
      this.$emit('deleteTodo', index)
    }
  }
}
</script>
