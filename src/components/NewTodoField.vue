<template>
  <div class="input-group mb-3">
    <input type="text" class="form-control" v-model="content" placeholder="Enter the contents of the to-do list." aria-label="Enter the contents of the to-do list." aria-describedby="button-addon2">
    <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="createTodo">Add ToDo</button>
  </div>
</template>

<script>
export default {
  name: 'NewTodoField',
  data () {
    return {
      content: '',
    }
  },
  methods: {
    createTodo () {
      this.$emit('addTodo', this.content)
      this.content = ''
    }
  }
}
</script>
