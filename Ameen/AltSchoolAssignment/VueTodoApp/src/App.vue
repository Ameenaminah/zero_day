<template>
  <div id="app">
    <div class="todo-container">
      <h1>My Todo App</h1>
      <div class="add-todo">
        <input
          v-model="newTodo"
          @keyup.enter="addTodo"
          placeholder="Add a new todo"
        />
        <button @click="addTodo">Add Todo</button>
      </div>
      <todo-list :todos="todos" @edit="editTodo" @delete="deleteTodo" />
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  components: {
    TodoList,
  },
  data() {
    return {
      newTodo: "",
      todos: [],
      nextId: 1,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === "") return;

      this.todos.push({
        id: this.nextId++,
        text: this.newTodo,
        completed: false,
      });

      this.newTodo = "";
    },
    editTodo(id, text) {
      const todo = this.todos.find((t) => t.id === id);
      if (todo) {
        todo.text = text;
      }
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin: 60px auto;
}
.todo-container {
  border: 5px solid black;
  padding: 4em;
}
h1 {
  font-size: 2em;
  color: #2c3e50;
  margin-bottom: 20px;
}
.add-todo {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-bottom: 2em;
}

input {
  padding: 10px;
  margin-right: 8px;
}

button {
  padding: 10px;
  background-color: #3498db;
  color: #fff;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #ecf0f1;
  padding: 10px;
  margin: 8px 0;
  border-radius: 4px;
}

.todo-item span {
  flex-grow: 1;
  text-align: left;
}

.todo-item button {
  background-color: #e74c3c;
  color: #fff;
  border: none;
  margin-left: 8px;
}

.todo-item button:hover {
  background-color: #c0392b;
}
</style>
