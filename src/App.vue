<template>
  <div>
    <input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo" />
    <ul class="todos">
      <li
        v-for="todo in todos"
        :key="todo.id"
        @dblclick="toggleEditMode(todo)"
        :class="{complete: todo.completed}"
      >
        <input
          v-model="todo.label"
          @keydown.enter="confirmChange(todo)"
          v-if="todo.isEditable"
          placeholder="New label"
        />
        <h3>{{ todo.label }}</h3>
        <div>
          <button @click="removeTodo(todo.id)">🚮</button>
          <button @click="completeTodo(todo)">✅</button>
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
        completed: false,
        isEditable: false
      });
      this.currentTodo = "";
    },
    removeTodo(id) {
      this.todos.splice(id, 1);
    },
    toggleEditMode(todo) {
      todo.isEditable = !todo.isEditable;
    },
    confirmChange(todo) {
      todo.isEditable = false;
    },
    completeTodo(todo) {
      todo.completed = true;
    }
  }
};
</script>

<style>
.complete {
    background-color: aquamarine;
}
</style>
