<template>
  <footer>
    <div class="author-text">
      <p>Made with ❤️ by <a href="https://shikharbaniya.netlify.app" target="_blank"><b>Shikhar Baniya</b></a>
      </p>
    </div>
  </footer>

  <div class="container">
    <header>
      <h1>TodoZen</h1>
      <!-- Error message -->
      <div class="alert-message">
        <div v-if="isAlertVisible" class="alert shadow-lg mb-5 w-full" :class="alertClass">
          <div>
            <span>{{ alertMessage }}</span>
          </div>
        </div>
      </div>
      <div class="input-section">
        <input v-model="newTodo" type="text" @keyup.enter="addTodo" placeholder="Add a todo . . ."
          class="input input-bordered input-secondary w-full max-w-xs" />
        <input v-model="newDate" type="date"
          class="input input-bordered input-secondary w-full max-w-xs"/>
        <button class="btn btn-secondary add-task-button" @click="isEditing ? handleEdit() : addTodo()">
          <i class="bx bx-sm" :class="addTodoClass"></i>
        </button>
      </div>
    </header>

    <div class="todos-filter">
      <div class="dropdown">
        <label tabindex="0" class="btn m-1">Filter</label>
        <ul tabindex="0" class="dropdown-content menu p-2 shadow bg-base-100 rounded-box w-52">
          <li @click="filterTodos('all')"><a>All</a></li>
          <li @click="filterTodos('pending')"><a>Pending</a></li>
          <li @click="filterTodos('completed')"><a>Completed</a></li>
        </ul>
      </div>
      <button class="btn btn-secondary delete-all-btn" @click="reset">
        Delete All
      </button>
    </div>

    <table class="table w-full">
      <thead>
        <tr>
          <th>Task</th>
          <th>Due Date</th>
          <th>Status</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody v-if="loadTodosFromLocalStorage" class="todos-list-body">
        <tr v-for="(todo, index) in todoList" :key="index">
          <td :title="todo.task">{{ formatTask(todo.task) }}</td>
          <td>{{ formatDate(todo.date) }}</td>
          <td>{{ todo.status }}</td>
          <td>
            <button title="Edit" class="btn btn-warning btn-sm mr-2" @click="edit(index)">
              <i class="bx bx-edit-alt bx-bx-xs"></i>
            </button>
            <button v-if="todoList[index].status == 'Pending'" title="Complete" class="btn btn-success btn-sm mr-2" @click="updateStatus(index)">
              <i class="bx bx-check bx-xs"></i>
            </button>
            <button v-else title="Pending" class="btn btn-info btn-sm mr-2" @click="updateStatus(index)">
              <i class='bx bxs-error-circle bx-xs'></i>
            </button>
            <button title="Delete" class="btn btn-error btn-sm" @click="remove(index)">
              <i class="bx bx-trash bx-xs"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  
  <ThemeSwitcher />
</template>

<script>
import ThemeSwitcher from '../components/themeSwitcher.vue';

export default {
  name: 'App',
  components: {
    ThemeSwitcher
  },
  data() {
    return {
      newTodo: '',
      newDate: '',
      todoList: [],
      alertMessage: '',
      isAlertVisible: false,
      alertClass: '',
      addTodoClass: 'bx-plus',
      isEditing: false,
      editIndex: null
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todoList.push({ task: this.newTodo, date: this.newDate, completed: false, status: 'Pending' });
        this.newTodo = '';
        this.newDate = '';
        this.showAlert("Task Added Successfully", "alert-success");
        this.saveTodosToLocalStorage();
      } else {
        this.showAlert("Please Add Some Tasks", "alert-warning");
      }
    },
    remove(index) {
      this.todoList.splice(index, 1)
      this.saveTodosToLocalStorage();
    },
    updateStatus(index) {
      this.todoList[index].status = this.todoList[index].status === 'Completed' ? 'Pending' : 'Completed';
      this.todoList[index].completed = !this.todoList[index].completed;
      this.saveTodosToLocalStorage();
    },
    edit(index) {
      this.editIndex = index;
      this.isEditing = true;
      this.newTodo = this.todoList[index].task;
      this.addTodoClass = 'bx-check'
    },
    handleEdit() {
      if (this.newTodo.trim() == '' || this.newDate == '') {
        this.showAlert("Please Add Some Tasks!!", "alert-warning");
      } else {
        if(this.newTodo === this.todoList[this.editIndex].task && this.newDate === this.todoList[this.editIndex].date) {
          this.showAlert("No Changes has been done", "alert-warning");
        } else {
          this.todoList[this.editIndex].task = this.newTodo;
          this.todoList[this.editIndex].date = this.newDate ? this.newDate : '';
          this.isEditing = false;
          this.newTodo = '';
          this.addTodoClass = 'bx-plus';
          this.saveTodosToLocalStorage();
          this.showAlert("Task Updated Successfully", "alert-success");
        }
      }
    },
    reset() {
      this.todoList = [];
      this.saveTodosToLocalStorage();
    },
    showAlert(message, type){
      this.isAlertVisible = true;
      this.alertMessage = message;
      this.alertClass = type;
      setTimeout(() => {
        this.isAlertVisible = false;
        this.alertMessage = '';
      }, 3000);
    },
    saveTodosToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todoList));
    },
    retrieveTodosFromLocalStorage() {
      const todos = localStorage.getItem('todos');
      if (todos) {
        this.todoList = JSON.parse(todos);
      }
    },
    filterTodos(status){
      const todos = JSON.parse(localStorage.getItem('todos'));

      switch(status) {
        case 'all' :
          this.todoList = todos; break;
        case 'pending' :
          this.todoList = todos.filter((todo) => !todo.completed); break;
        case 'completed' : 
          this.todoList = todos.filter((todo) => todo.completed); break;
        default :
          this.todoList = [];
      }
    }
  },
  computed: {
    formatTask(){
      return (task) => {
        return task.length > 20 ? task.substring(0, 20) + "..." : task;
      }
    },
    formatDate() {
      return (date) => {
        return date || "No Due Date";
      }
    },
    loadTodosFromLocalStorage() {
      this.retrieveTodosFromLocalStorage();
      return true;
    }  
  }
}
</script>

<style src="./assets/style.css" />
