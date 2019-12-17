<template>
  <div>
    <md-card class="md-layout-item md-large-size-50 md-medium-size-75 md-small-size-100">
      <md-card-header>
        <div class="md-title">To-Do List</div>
        <md-field>
          <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a to-do"></md-input>
        </md-field>
      </md-card-header>
      <md-card-content>
        <md-list class="todos">
          <md-list-item v-for="todo in todos" :key="todo.id">
            <input type="checkbox" v-model="todo.completed">
            <span v-if="!todo.edit">
              {{ todo.label }}
            </span>
            <input v-else type="text" v-model="todo.label" @keydown.enter="doneEditing(todo)">
            <div>
              <md-button class="md-icon-button" @click="editTodo(todo)"><md-icon>edit</md-icon></md-button>
              <md-button class="md-icon-button md-accent" @click="removeTodo(todo)"><md-icon>delete</md-icon></md-button>
            </div>
          </md-list-item>
        </md-list>
      </md-card-content>
    </md-card>
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

.md-card {
  margin: auto;
}

.md-title{
  font-family: 'Shadows Into Light', cursive;
}
</style>
