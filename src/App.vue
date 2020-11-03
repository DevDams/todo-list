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
import axios from 'axios'

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
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(response => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(e => console.log(e))

      // this.todos = this.todos.filter(todo => todo.id !== id)
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(response => this.todos = [...this.todos, response.data])
      .catch(e => console.log(e))

      // this.todos = [...this.todos, response.data]
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(response => {
      // JSON responses are automatically parsed.
      this.todos = response.data
    })
    .catch(e => console.log(e))
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
