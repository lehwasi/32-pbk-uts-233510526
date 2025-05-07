<template>
  <div class="container">
    <h1 class="title">To-Do List</h1>

    <div class="input-group">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        class="todo-input"
        placeholder="Tambah tugas..."
      />
    </div>

    <div class="filter-buttons">
      <button
        @click="filter = 'all'"
        :class="{ active: filter === 'all' }"
      >Semua</button>
      <button
        @click="filter = 'active'"
        :class="{ active: filter === 'active' }"
      >Belum Selesai</button>
    </div>

    <ul class="todo-list" v-if="filteredTodos.length">
      <li v-for="todo in filteredTodos" :key="todo.id" class="todo-item">
        <input type="checkbox" v-model="todo.completed" />
        <span :class="{ done: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(todo.id)" class="delete-button">🗑️</button>
      </li>
    </ul>
    <p v-else class="empty-message">Tidak ada tugas yang ditampilkan</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      filter: 'all'
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'active') {
        return this.todos.filter(todo => !todo.completed)
      }
      return this.todos
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === '') return
      this.todos.push({
        id: Date.now(),
        text: this.newTodo,
        completed: false
      })
      this.newTodo = ''
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 500px;
  margin: 40px auto;
  padding: 20px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', sans-serif;
}

.title {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

.input-group {
  display: flex;
  justify-content: center;
  margin-bottom: 15px;
}

.todo-input {
  padding: 10px;
  width: 100%;
  border: 2px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
}

.filter-buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

.filter-buttons button {
  padding: 8px 16px;
  border: none;
  background-color: #eee;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
}

.filter-buttons button.active {
  background-color: #3498db;
  color: white;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #f9f9f9;
  padding: 12px;
  margin-bottom: 10px;
  border-radius: 8px;
  transition: background 0.3s;
}

.todo-item:hover {
  background: #f1f1f1;
}

.todo-item span {
  flex: 1;
  margin-left: 10px;
}

.done {
  text-decoration: line-through;
  color: #888;
}

.delete-button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 18px;
  color: red;
}

.empty-message {
  text-align: center;
  color: #999;
}
</style>
