<template>
  <li class="list-group-item">
    <input type="text" class="form-control"
           v-if="editFlg"
           :value="content"
           @keypress.enter="updateTodo">
    <span v-if="editFlg">(編集完了後、Enterキーを押すと更新されます)</span>

    <p v-if="!editFlg">{{ content }}</p>
    <EditButton v-if="!editFlg"
                @toggle-edit-flg="toggleEditFlg" />
    <DeleteButton v-if="!editFlg"
                  @delete-todo="deleteTodo" />
  </li>
</template>

<script>
import EditButton from "./EditButton.vue"
import DeleteButton from "./DeleteButton.vue"

export default {
  name: 'ListItem',
  props: ['index', 'content'],
  components: {
    EditButton,
    DeleteButton
  },
  data () {
    return {
      editFlg: false
    }
  },
  methods: {
    updateTodo (e) {
      this.$emit('updateTodo', this.index, e.target.value)
      this.editFlg = !this.editFlg
    },
    deleteTodo () {
      this.$emit('deleteTodo', this.index)
    },
    toggleEditFlg () {
      this.editFlg = !this.editFlg
    }
  }
}
</script>
