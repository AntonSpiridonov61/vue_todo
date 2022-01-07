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
      <task-form
        @edit="editTask"
      />
    </my-dialog>
    <task-list 
      :tasks="sortedTasks"
      @remove="removeTask"
    />
  </div>
</template>

<script>
import TaskList from "./components/TaskList";
import TaskForm from "./components/TaskForm";
export default {
  components: {
    TaskList, TaskForm
  },
  data() {
    return {
      tasks: [],
      dialogCreateVisible: false,
      dialogEditVisible: false,
      selectedSort: "",
      sortOptions: [
        {value: "title", name: "По названию"},
        {value: "body", name: "По описанию"},
      ]
    }
  },
  methods: {
    createTask(task) {
      this.tasks.push(task);
      this.dialogCreateVisible = false;
    },
    removeTask(task) {
      this.tasks = this.tasks.filter(item => item.id !== task.id);
    },
    editTask(task) {
      
    },
    showDialog() {
      this.dialogCreateVisible = true;
    }
  },
  computed: {
    sortedTasks() {
      return [...this.tasks].sort((task1, task2) => {
        return task1[this.selectedSort]?.localeCompare(task2[this.selectedSort])
      })
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

.app_btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
</style>
