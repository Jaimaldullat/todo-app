<template>
  <div class="container">
    <h1>Todo App</h1>
    <TodoForm @add-todo="addTodo" />
    <TodoTabs v-model="activeTab" />
    <TodoList 
      :todos="filteredTodos" 
      @toggle-todo="toggleTodo"
      @delete-todo="deleteTodo"
    />
  </div>
</template>

<script>
import TodoForm from './components/TodoForm.vue'
import TodoList from './components/TodoList.vue'
import TodoTabs from './components/TodoTabs.vue'

export default {
  name: 'App',
  components: {
    TodoForm,
    TodoList,
    TodoTabs
  },
  data() {
    return {
      todos: [],
      activeTab: 'all'
    }
  },
  computed: {
    filteredTodos() {
      switch (this.activeTab) {
        case 'active':
          return this.todos.filter(todo => !todo.completed)
        case 'completed':
          return this.todos.filter(todo => todo.completed)
        default:
          return this.todos
      }
    }
  },
  methods: {
    addTodo(text) {
      this.todos.push({
        id: Date.now(),
        text,
        completed: false
      })
    },
    toggleTodo(id) {
      const todo = this.todos.find(todo => todo.id === id)
      if (todo) todo.completed = !todo.completed
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  color: #2c3e50;
}
</style>
