<template>
  <div class="app">
    <my-button class="btn_create" @click="showDialog">Создать задачу</my-button>
    <my-dialog v-model:show="dialogVisible">
      <task-form
        @create="createTask"
      />
    </my-dialog>
    <task-list 
      :tasks="tasks"
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
      dialogVisible: false
    }
  },
  methods: {
    createTask(task) {
      this.tasks.push(task);
      this.dialogVisible = false;
    },
    removeTask(task) {
      this.tasks = this.tasks.filter(item => item.id !== task.id);
    },
    showDialog() {
      this.dialogVisible = true;
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

.btn_create {
  margin: 15px 0;
}
</style>
