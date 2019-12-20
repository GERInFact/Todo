<template>
  <div>
    <md-field>
      <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo"></md-input>
    </md-field>
    <ul class="todos md-layout md-gutter md-alignment-center">
      <md-list
        v-for="todo in todos"
        :key="todo.id"
        @dblclick="toggleEditMode(todo)"
        class="md-layout-item md-medium-size-33 md-small-size-50 md-xsmall-size-100"
        :class="{complete: todo.completed}"
      >
        <md-list-item>
          <md-field>
            <md-input
              v-model="todo.label"
              @keydown.enter="confirmChange(todo)"
              v-if="todo.isEditable"
              placeholder="New label"
              class="edit"
            ></md-input>
          </md-field>
        </md-list-item>

        <h3>{{ todo.label }}</h3>
        <md-list-item>
          <md-button @click="removeTodo(todo.id)">
            <md-icon class="md-primary">delete</md-icon>
          </md-button>
          <md-button @click="mark(todo)">
            <md-icon class="md-accent md-raised">verified_user</md-icon>
          </md-button>
        </md-list-item>
      </md-list>
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
    mark(todo) {
      todo.completed = !todo.completed;
    }
  }
};
</script>

<style>
ul {
  margin: 0;
  padding: 20px;
}
md-list {
  margin: 0 5px;
  padding: 10px;
  box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0.35);
}
.edit {
  padding: 5px !important;
  background-color: rgba(255, 255, 255, 0.1) !important;
}
.edit .md-field:after {
  height: 0;
}
.complete {
  background-color: rgba(127, 255, 212, 0.37);
}
</style>
