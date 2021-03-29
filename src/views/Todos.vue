<template>
  <div>
    <h2>To do Application</h2>
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
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => this.todos = json)
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

<style scoped>

</style>