<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from './components/layout/Header'
import AddTodo from './components/AddTodo'
import Todos from './components/Todos'

export default {
  name: 'App',
  components: {
    Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: 'Todos one',
          completed: false
        },
        {
          id: 2,
          title: 'Todos two',
          completed: false
        },
        {
          id: 3,
          title: 'Todos three',
          completed: false
        }
      ]
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo]
      this.title = ''
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #f2f2f2;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
