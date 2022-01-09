<template>
  <div class="app container-sm">
    <h2>TODO List</h2>
    <div class="row">
      <my-button class="btn-success col-auto me-auto" @click="showCreateDialog">Создать задачу</my-button>
      <my-select v-model="selectedSort" :options="sortOptions"/>
      <my-button class="btn-danger col-auto" @click="clearAllTasks">Удалить все записи</my-button>
    </div>
    <br><h3>Список задач</h3>
    <my-dialog 
      v-model:show="dialogCreateVisible"
      :title="createTitle"
      >
      <task-create-form
        @create="createTask"
      />
    </my-dialog>
    <my-dialog 
      v-model:show="dialogEditVisible"
      :title="editTitle"
      >
      <task-edit-form
        :selectedTask="selectedTask"
        @edit="editTask"
      />
    </my-dialog>
    <task-list 
      :tasks="sortedTasks"
      @showEditDialog="showEditDialog"
      @remove="removeTask"
    />
  </div>
</template>

<script>
import TaskList from "./components/TaskList";
import TaskCreateForm from "./components/TaskCreateForm";
import TaskEditForm from "./components/TaskEditForm";
export default {
  components: {
    TaskList, TaskCreateForm, TaskEditForm
  },
  data() {
    return {
      tasks: [],
      selectedTask: {},
      dialogCreateVisible: false,
      dialogEditVisible: false,
      selectedSort: "",
      sortOptions: [
        {value: "all", name: "Все"},
        {value: "done", name: "Выполненые"},
        {value: "active", name: "Активные"},
        {value: "title", name: "По названию"},
        {value: "body", name: "По описанию"},
        {value: "priority", name: "По приоритету"}
      ],
      createTitle: "Создание задачи",
      editTitle: "Изменение задачи"
    }
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
    }
  },
  methods: {
    showCreateDialog() {
      this.dialogCreateVisible = true;
    },
    createTask(task) {
      this.tasks.push(task);
      this.saveLocalStorageTasks();
      this.dialogCreateVisible = false;
    },
    removeTask(task) {
      this.tasks = this.tasks.filter(item => item.id !== task.id);
      this.saveLocalStorageTasks();
    },
    showEditDialog(task) {
      this.selectedTask = task;
      this.dialogEditVisible = true;
    },
    editTask(editTask) {
      const Task = this.tasks.find(task => task.id === editTask.id)
      Task.title = editTask.title;
      Task.body = editTask.body;
      Task.priority = editTask.priority;
      Task.is_done = editTask.is_done;
      
      this.saveLocalStorageTasks();
      this.dialogEditVisible = false;
    },
    clearAllTasks() {
      this.tasks = [];
      this.saveLocalStorageTasks();
    },
    saveLocalStorageTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
    }
  },
  computed: {
    sortedTasks() {
      switch (this.selectedSort) {
        case 'done':
          return [...this.tasks].filter((task) => task.is_done);
        case 'active':
          return [...this.tasks].filter((task) => !task.is_done);
        case 'priority':
          return [...this.tasks].sort((task1, task2) => {
            return task2.priority.value - task1.priority.value
          })
        case 'title':
        case 'body':
          return [...this.tasks].sort((task1, task2) => {
            return task1[this.selectedSort]?.localeCompare(task2[this.selectedSort])
          })
        case 'all':
        default:
          return [...this.tasks]
      }
    }
  }
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
</style>
