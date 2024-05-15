<template>
  <div class="app">
    <h1 class="title">Todo List</h1>
    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" class="todo-item" @mouseover="hoverTodoItem(todo.id, true)" @mouseleave="hoverTodoItem(todo.id, false)">
        <span class="todo-title">{{ todo.title }}</span>
        <div class="todo-actions" v-if="hoveredTodo === todo.id">
          <button class="edit-btn" @click="editTodo(todo)">Edit</button>
          <button class="delete-btn" @click="deleteTodo(todo)">Delete</button>
        </div>
      </li>
    </ul>
    <form @submit.prevent="addTodo">
      <input v-model="newTodoTitle" type="text" class="input-field" placeholder="Enter new todo">
      <button class="add-btn" type="submit">Add Todo</button>
    </form>
    <form v-if="editingTodo" @submit.prevent="updateTodo">
      <input v-model="editingTodo.title" type="text" class="input-field" placeholder="Edit todo">
      <button class="update-btn" type="submit">Update Todo</button>
      <button class="cancel-btn" @click="cancelEdit">Cancel</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { title: 'Belajar Vue', id: 1 },
        { title: 'Belajar React', id: 2 }
      ],
      newTodoTitle: '',
      editingTodo: null,
      hoveredTodo: null
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ title: this.newTodoTitle, id: Date.now() })
      this.newTodoTitle = ''
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter(t => t.id !== todo.id)
    },
    editTodo(todo) {
      this.editingTodo = todo
    },
    updateTodo() {
      this.editingTodo = null
    },
    cancelEdit() {
      this.editingTodo = null
    },
    hoverTodoItem(todoId, isHovered) {
      this.hoveredTodo = isHovered ? todoId : null;
    }
  }
}
</script>

<style>
.app {
  max-width: 400px;
  margin: 40px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #f4f4f4; /* Warna latar belakang abu-abu */
}

.title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 20px;
  color: #4CAF50;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  position: relative;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  transition: background-color 0.3s;
}

.todo-item:hover {
  background-color: #f0f0f0;
}

.todo-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #000; /* Warna teks hitam */
}

.todo-actions {
  position: absolute;
  top: 50%;
  right: 20px;
  transform: translateY(-50%);
  opacity: 0;
  transition: opacity 0.3s;
}

.todo-item:hover .todo-actions {
  opacity: 1;
}

.edit-btn,
.delete-btn,
.add-btn,
.update-btn,
.cancel-btn {
  background-color: #4CAF50;
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.edit-btn:hover,
.delete-btn:hover,
.add-btn:hover,
.update-btn:hover,
.cancel-btn:hover {
  background-color: #3e8e41;
}

.input-field {
  width: calc(100% - 110px); /* Disesuaikan dengan lebar field input */
  height: 40px;
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.add-btn {
  width: 100px; /* Disesuaikan dengan lebar field input */
}
</style>
