<template>
  <a @click="deleteTodo">
    <i class="bi bi-trash-fill"></i>削除
  </a>
</template>

<script>
export default {
  name: 'DeleteButton',
  methods: {
    deleteTodo () {
      this.$emit('deleteTodo')
    }
  }
}
</script>

<style>
a:hover {
  cursor: pointer;
}
</style>
