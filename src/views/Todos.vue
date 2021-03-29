<template>
  <div>
    <h2>To do Application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
        v-on:add-todo="addTodo"
    />
    <hr>
    <Loader v-if="loading"/>
    <TodoList
        v-else-if="todos.length"
        v-bind:todos="todos"
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
      loading: true
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=150')
        .then(response => response.json())
        .then(json => {
          this.todos = json
          this.loading = false
        })
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