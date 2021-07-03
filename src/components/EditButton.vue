<template>
  <a @click="toggleEditFlg">
    <i class="bi bi-pencil-fill"></i>編集
  </a>
</template>

<script>
export default {
  name: 'EditButton',
  methods: {
    toggleEditFlg () {
      this.$emit('toggleEditFlg')
    }
  }
}
</script>

<style>
a:hover {
  cursor: pointer;
}
</style>
