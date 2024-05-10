<template>
  <div class="container">
    <form @submit.prevent="tambah" class="todo-form">
      <input v-model="newTodo" placeholder="Add a new todo" class="todo-input">
      <button class="add-btn">Add</button>
    </form>

    <ol class="todo-list">
      <li v-for="todo in filteredTodos" :key="todo.id" class="todo-item">
        <input type="checkbox" v-model="todo.done" class="todo-checkbox">
        <span :class="{ 'todo-text': true, 'done': todo.done }">{{ todo.text }}</span>
        <div class="btn-group">
          <button @click="edit(todo)" class="edit-btn">Edit</button>
          <button @click="hapus(todo)" class="delete-btn">Delete</button>
        </div>
      </li>
    </ol>

    <button @click="hideCompleted = !hideCompleted" class="toggle-btn">
      {{ hideCompleted ? 'Show All' : 'Hide Completed' }}
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

let id = ref(0)
const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
    { id: id.value++, text: 'Membuat Tugas PBK', done: true },
    { id: id.value++, text: 'Membuat Tugas PBO', done: true },
    { id: id.value++, text: 'Membuat Tugas DAA', done: false }
])

const tambah = () => {
  if (newTodo.value.trim() !== '') { 
    todos.value.push({ id: id.value++, text: newTodo.value })
    newTodo.value = ''
  } else {
    alert('Isi Bidang Ini!!!') 
  }
}

const hapus = (todo) => {
  todos.value = todos.value.filter(t => t !== todo)
}

const edit = (todo) => {
  const newText = prompt('Edit todo:', todo.text)
  if (newText !== null) {
    todo.text = newText
  }
}

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter(t => !t.done)
    : todos.value
})
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}


.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #dedede;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  transform: translateX(5%);
}

.title {
  font-family: Georgia, "Times New Roman", Times, serif;
  text-align: center;
}

.form-container {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.form-container p {
  font-family: sans-serif;
}

.text-input {
  width: 95%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  transition: border-color 0.3s ease;
  word-wrap: break-word;
}

.text-input:focus {
  border-color: #2f8e28;
}

.highlight {
  background-color: yellow;
}

p {
  margin: 10px 0;
  color: #555;
}

.wrapped-text {
  display: block;
  max-width: 100%;
  overflow-wrap: break-word;
  font-family: "Courier New", Courier, monospace;
}

.option-group {
  margin-top: 20px;
}

.option-group p {
  font-weight: bold;
}

.option-group button {
  margin-right: 10px;
}

/* Root CSS */
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Additional Styles */
.todo-form {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
}

.todo-input {
  padding: 12px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 200px;
}

.add-btn {
  padding: 12px 24px;
  font-size: 16px;
  background-color: #2ecc71;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-btn:hover {
  background-color: #27ae60;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  margin-bottom: 12px;
}

.todo-checkbox {
  margin-right: 12px;
}

.todo-text {
  flex: 1;
  font-size: 16px;
  color: #333;
}

.todo-text.done {
  text-decoration: line-through;
  color: #888;
}

.btn-group button {
  margin-left: 8px;
  padding: 8px 16px;
  font-size: 14px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.edit-btn {
  background-color: #f39c12;
  color: white;
}

.edit-btn:hover {
  background-color: #d35400;
}

.delete-btn {
  background-color: #e74c3c;
  color: white;
}

.delete-btn:hover {
  background-color: #c0392b;
}

.toggle-btn {
  padding: 12px 24px;
  font-size: 16px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.toggle-btn:hover {
  background-color: #2980b9;
}

</style>
