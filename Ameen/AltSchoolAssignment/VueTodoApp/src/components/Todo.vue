<template>
  <div class="todo-item">
    <span v-if="!editing">{{ todo.text }}</span>
    <input v-if="editing" v-model="editedText" @keyup.enter="saveEdit" @blur="saveEdit" />
    <button @click="toggleEdit">{{ editing ? 'Finish' : 'Edit' }}</button>
    <button @click="deleteTodo">Delete</button>
  </div>
</template>

<script>
export default {
  props: ['todo'],
  data() {
    return {
      editing: false,
      editedText: this.todo.text,
    };
  },
  methods: {
    toggleEdit() {
      if (this.editing) {
        this.saveEdit();
      } else {
        this.editing = true;
      }
    },
    saveEdit() {
      this.$emit('edit', this.todo.id, this.editedText);
      this.editing = false;
    },
    deleteTodo() {
      this.$emit('delete', this.todo.id);
    },
  },
};
</script>

<style scoped>
.todo-item {
  margin-bottom: 8px;
}
</style>
