<template>
  <div>
    <todo
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @edit="editTodo"
      @delete="deleteTodo"
    />
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  components: {
    Todo,
  },
  props: ["todos"],
  methods: {
    editTodo(id, text) {
      this.$emit("edit", id, text);
    },
    deleteTodo(id) {
      this.$emit("delete", id);
    },
  },
};
</script>
