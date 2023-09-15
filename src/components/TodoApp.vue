
<template class="body">
  <div class="container">
    <h2 class="text-center mt-5">Enhanced Vue.js Task List</h2>
    <div class="d-flex p-3 m-3">
      <input type="text" v-model="task" placeholder="Enter Task Name" class="form-control">
      <button @click="addTask" class="btn btn-dark rounded-0">Add Task</button>
    </div>

    <!-- Filter buttons -->
    <div class="mb-3">
      <button @click="filterCompletedTasks" class="btn btn-primary p-2 m-2">Completed Tasks</button>
      <button @click="showAllTasks" class="btn btn-primary p-2 m-2">All Tasks</button>
    </div>

    <table class="table table-dark table-hover mt-3">
      <thead>
        <tr>
          <th scope="col" class="text-center">Task</th>
          <th scope="col" class="text-center">Status</th>
          <th scope="col" class="text-center">To Edit</th>
          <th scope="col" class="text-center">To Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in filteredTasks" :key="index">
          <td>{{ task.name }}</td>
          <td>
            <span class="pointer" @click="changeStatus(index)">
              {{ task.status }}
            </span>
          </td>
          <td>
            <div class="text-center pointer" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center pointer" @click="deleteTask(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      task: "",
      editedTask: null,
      avaiableStatusOptions: ['just started', 'pending', 'completed'],
      tasks: [
        {
          name: "go to Shopping",
          status: "just started",
        },
        {
          name: "finish my Python project",
          status: "completed"
        },
        {
          name: "finish my Java project",
          status: "completed"
        },
        {
          name: "finish my Node Js project",
          status: "completed"
        },
        {
          name: "finish my C project",
          status: "pending"
        },
        {
          name: "finish my React jsproject",
          status: "completed"
        },
        {
          name: "finish my Next js project",
          status: "pending"

        },
        {
          name: "finish my MongoDB course",
          status: "completed"
        }
      ],
      // Initially, display all tasks
      filteredStatus: null,
    }
  },
  computed: {
    filteredTasks() {
      if (this.filteredStatus === null) {
        return this.tasks;
      } else {
        return this.tasks.filter(task => task.status === this.filteredStatus);
      }
    }
  },
  methods: {
    addTask() {
      if (this.task.length === 0) {
        alert("A task without a name cannot exist");
        return;
      }

      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "just started"
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index) {
      let caughtIndex = this.avaiableStatusOptions.indexOf(this.tasks[index].status);

      if (++caughtIndex > 2) {
        caughtIndex = 0;
      }

      this.tasks[index].status = this.avaiableStatusOptions[caughtIndex];
    },
    filterCompletedTasks() {
      this.filteredStatus = 'completed';
    },
    showAllTasks() {
      this.filteredStatus = null;
    }
  }
}
</script>

<style scoped>
.body{
  margin-top: 20%;
}
.pointer {
  cursor: pointer;
}

/* Custom CSS styling */
.container {
  background-color: #f2f2f2;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);


  height: 100vh;

}

.form-control {
  width: 70%;
}

.btn {
  border-radius: 0;
  font-weight: bold;
  border-radius: 5%;
}

.table {
  background-color: #333;
}

.table th {
  background-color: #444;
  color: #fff;
}

.table td {
  background-color: #555;
  color: #fff;
}

.btn-primary {
  background-color: #007bff;
  color: #fff;
}

.btn-primary:hover {
  background-color: #0056b3;
}
</style>
