<template>
  <div class="app">
    <h2>TODO List</h2>
    <div class="app_btns">
      <my-button @click="showDialog">Создать задачу</my-button>
      <my-select v-model="selectedSort" :options="sortOptions"/>
    </div>
    <my-dialog v-model:show="dialogCreateVisible">
      <task-form
        @create="createTask"
      />
    </my-dialog>
    <my-dialog v-model:show="dialogEditVisible">
      <task-edit-form
        :selectTask="selectTask"
        @saveTask="saveTask"
      />
    </my-dialog>
    <task-list 
      :tasks="sortedTasks"
      @edit="editTask"
      @remove="removeTask"
    />
  </div>
</template>

<script>
import TaskList from "./components/TaskList";
import TaskForm from "./components/TaskForm";
import TaskEditForm from "./components/TaskEditForm";
export default {
  components: {
    TaskList, TaskForm, TaskEditForm
  },
  data() {
    return {
      tasks: [],
      selectTask: {},
      dialogCreateVisible: false,
      dialogEditVisible: false,
      selectedSort: "",
      sortOptions: [
        {value: "title", name: "По названию"},
        {value: "body", name: "По описанию"},
        {value: "id", name: "По id"},
        {value: "priority.value", name: "По приоритету"},
      ],
    }
  },
  methods: {
    createTask(task) {
      this.tasks.push(task);
      this.saveLocalStorageTodos();
      this.dialogCreateVisible = false;
    },
    removeTask(task) {
      this.tasks = this.tasks.filter(item => item.id !== task.id);
      this.saveLocalStorageTodos();
    },
    editTask(task) {
      this.selectTask = task;
      this.dialogEditVisible = true;
    },
    saveTask(editTask) {
      const Task = this.tasks.find(task => task.id === editTask.id)
      Task.title = editTask.title;
      Task.body = editTask.body;
      Task.priority = editTask.priority;
      Task.is_done = editTask.is_done;
      
      this.saveLocalStorageTodos();
      this.dialogEditVisible = false;
    },
    showDialog() {
      this.dialogCreateVisible = true;
    },
    saveLocalStorageTodos() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
    }
  },
  computed: {
    sortedTasks() {
      return [...this.tasks].sort((task1, task2) => {
        return task1[this.selectedSort]?.localeCompare(task2[this.selectedSort])
      })
    }
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
    }
  },
}
</script>


<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.app_btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
</style>
