<template>
  <div>
    <input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo" />
    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        <h3>{{ todo.label }}</h3>
        <div>
          <button @click="removeTodo(todo.id)">🚮</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: ""
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false
      });
      this.currentTodo = "";
    },
    removeTodo(id) {
      this.todos.splice(id, 1);
    }
  }
};
</script>

<style>
</style>
