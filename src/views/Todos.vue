<template>
  <div>
    <h2>To do Application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>

    </select>
    <AddTodo
        v-on:add-todo="addTodo"
    />
    <hr>
    <Loader v-if="loading"/>
    <TodoList
        v-else-if="filteredTodos.length"
        v-bind:todos="filteredTodos"
        v-on:remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader"

export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id: 1, title: 'Купить хлеб', completed: false},
        {id: 2, title: 'Купить колбасу', completed: false},
        {id: 3, title: 'Купить молоко', completed: false},
      ],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.todos = json
            this.loading = false
          }, 1000)
        })
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      }
      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }
      if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
      else return 0
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id != id)
    },

    addTodo(el) {
      this.todos.push(el)
    }
  },
  components: {
    AddTodo,
    TodoList,
    Loader
  }
}
</script>

<style scoped>

</style>