<template>
  <div>
    <h1>To-Do List</h1>
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Tambah tugas..." />
    
    <div>
      <button @click="filter = 'all'">Semua</button>
      <button @click="filter = 'active'">Belum Selesai</button>
    </div>

    <ul v-if="filteredTodos.length">
      <li v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.completed" />
        <span :style="{ textDecoration: todo.completed ? 'line-through' : 'none' }">
          {{ todo.text }}
        </span>
        <button @click="removeTodo(todo.id)">Hapus</button>
      </li>
    </ul>
    <p v-else>Tidak ada tugas yang ditampilkan</p>
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
        return this.todos.filter(todo => !todo.completed);
      }
      return this.todos;
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === '') return;
      this.todos.push({
        id: Date.now(),
        text: this.newTodo,
        completed: false
      });
      this.newTodo = '';
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
}
</script>
