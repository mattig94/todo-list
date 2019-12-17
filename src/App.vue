<template>
  <div>
    <input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo">
    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.completed">
        <span @dblclick="editTodo(todo)" v-if="!todo.edit">
          {{ todo.label }}
        </span>
        <input v-else type="text" v-model="todo.label" @keydown.enter="doneEditing(todo)">
        <button @click="removeTodo(todo)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, edit: false});
      this.currentTodo='';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.edit = true;
    },
    doneEditing(todo) {
      todo.edit = false;
    }
  }
};
</script>

<style>
li {
  list-style: none;
}
</style>
