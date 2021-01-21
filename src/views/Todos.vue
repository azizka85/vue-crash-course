<template>
  <div>
    <h2>Todo application</h2>
    <AddTodo 
      @add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr>
    <Loader v-if="loading" />
    <TodoList 
      v-else-if="filteredTodos.length"
      :todos="filteredTodos" 
      @remove-todo="removeTodo"
    />
    <p v-else>No todos</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  computed: {
    filteredTodos() {
      switch(this.filter) {
        case 'all':
        default:
          return this.todos
        case 'completed':
          return this.todos.filter(t => t.completed)
        case 'not-completed':
          return this.todos.filter(t => !t.completed)
      }
    } 
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
/*   watch: {
    filter(value) {
      console.log(value)
    }
  }, */
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json
          this.loading = false
        }, 1000)
      })
  }
}
</script>
