<template>
  <form @submit.prevent="handleSubmit" class="todo-form">
    <input 
      v-model="todoText"
      type="text"
      placeholder="Add a new todo"
      required
    >
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  name: 'TodoForm',
  data() {
    return {
      todoText: ''
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('add-todo', this.todoText)
      this.todoText = ''
    }
  }
}
</script>

<style scoped>
.todo-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #3aa876;
}
</style>
