<template>
  <div id="app">
    <h1>To do Application</h1>
    <AddTodo
      v-on:add-todo="addTodo"
    />
    <hr>
    <TodoList
      v-bind:todos="todos"
      v-on:remove-todo="removeTodo"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from "@/components/AddTodo";
export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id:1, title: 'Купить хлеб', completed: false},
        {id:2, title: 'Купить колбасу', completed: false},
        {id:3, title: 'Купить молоко', completed: false},
      ]
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
    TodoList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
