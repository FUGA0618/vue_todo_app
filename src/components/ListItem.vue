<template>
  <li class="list-group-item">
    <template v-if="editFlg">
      <input type="text" class="form-control"
             :value="content"
             @keypress.enter="updateTodo">
      <span>(編集完了後、Enterキーを押すと更新されます)</span>
    </template>

    <template v-else>
      <p>{{ content }}</p>
      <EditButton @click="toggleEditFlg" />
      <DeleteButton @click="deleteTodo" />
    </template>
  </li>
</template>

<script>
import EditButton from "./EditButton.vue"
import DeleteButton from "./DeleteButton.vue"

export default {
  name: 'ListItem',
  props: {
    index: {
      type: String,
      required: true,
      validator: value => {
        return parseInt(value)
      }
    },
    content: {
      type: String,
      required: true
    }
  },
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
      this.toggleEditFlg()
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
