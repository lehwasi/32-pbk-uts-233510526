<template>
  <div class="app">
    <h1>To-Do List</h1>
    <div class="input-section">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo" 
        placeholder="Tambahkan kegiatan baru..."
        class="task-input"
      />
      <button @click="addTodo" class="add-btn">Tambah</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
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
    }
  }
}
</script>
