<!-- TodoList.vue -->
<template>
   <div class="todo-list">
    <h2>Todo List</h2>
    <ul>
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        <div v-if="!todo.editMode">
          <input type="checkbox" v-model="todo.completed" class="checkbox" />
          <span :class="{ completed: todo.completed }">{{ todo.task }}</span>
          <button @click="toggleEditMode(todo)" class="edit-btn">Edit</button>
          <button @click="deleteTodo(todo.id)" class="delete-btn">Delete</button>
        </div>
        <div v-else>
          <input v-model="todo.updatedTask" placeholder="Edit task" />
          <button @click="updateTodo(todo)" class="update-btn">Update</button>
          <button @click="toggleEditMode(todo)" class="cancel-btn">Cancel</button>
        </div>
      </li>
    </ul>
    <div class="add-todo">
      <input v-model="newTodo" placeholder="Enter new task" />
      <button @click="addTodo" class="add-btn">Add Todo</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { id: 1, task: "Learn Vue.js", completed: false },
        { id: 2, task: "Build a Todo App", completed: true },
      ],
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push({
          id: this.todos.length + 1,
          task: this.newTodo,
          completed: false,
          editMode: false,
          updatedTask: "",
        });
        this.newTodo = "";
      }
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
    },
    toggleEditMode(todo) {
      todo.editMode = !todo.editMode;
      if (todo.editMode) {
        // Set the updated task to the current task value when entering edit mode
        todo.updatedTask = todo.task;
      }
    },
    updateTodo(todo) {
      // Update the task and exit edit mode
      todo.task = todo.updatedTask;
      todo.editMode = false;
    },
  },
};
</script>

<style scoped>
/* Add styling if needed */
.edit-btn,
.update-btn,
.cancel-btn,
.delete-btn {
  margin-left: 8px;
  padding: 6px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.edit-btn {
  background-color: #3498db;
  color: #fff;
}

.update-btn {
  background-color: #2ecc71;
  color: #fff;
}

.cancel-btn {
  background-color: #e74c3c;
  color: #fff;
}

.delete-btn {
  background-color: #e74c3c;
  color: #fff;
}

.update-btn,
.delete-btn {
  background-color: #42b983;
  color: #fff;
}
.cancel-btn {
  background-color: #ff6464;
  color: #fff;
}
.todo-list {
  max-width: 400px;
  margin: auto;
  
}
.todo-item {
  display: flex;
  align-items: center;
  padding: 8px;
  border: 1px solid #ddd;
  margin: 4px 0;
  background-color: #fff;
  border-radius: 4px;
}
.checkbox {
  margin-right: 8px;
}
.add-btn {
  background-color: #42b983;
  color: #fff;
  border: none;
  padding: 8px;
  border-radius: 4px;
  cursor: pointer;
}
input {
  padding: 8px;
  margin-right: 8px;
}
.delete-btn {
  background-color: #ff6464;
  color: #fff;
  border: none;
  padding: 6px;
  border-radius: 4px;
  cursor: pointer;
}
.add-todo {
  margin-top: 16px;
}
</style>
