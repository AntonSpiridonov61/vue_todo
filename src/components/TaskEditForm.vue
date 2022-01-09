<template>
  <form @submit.prevent>
    <label class="form-check-label">
      Состояние:
      <input class="form-check-input" type="checkbox" v-model="task.is_done">
    </label>
    <input
      v-model="task.title"
      class="input-group input-group-lg my-input"
      type="text"
      placeholder="Название"
    />
    <input
      v-model="task.body"
      class="input-group input-group-lg my-input"
      type="text"
      placeholder="Описание"
    />
    <my-radio v-model="task.priority" :radioOptions="radioOptions"/>
    <my-button 
      class="btn btn-outline-success" 
      style="margin-top: 15px;"
      @click="edit">Сохранить
    </my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      task: {
        title: '',
        body: '', 
        priority: {}, 
        is_done: false
      },
      radioOptions: [
        {value: "1", name: "Низкий"},
        {value: "2", name: "Средний"},
        {value: "3", name: "Высокий"},
      ],
    };
  },
  props: {
    selectedTask: {
      type: Object,
      required: true,
    }
  },
  mounted() {
    this.task.id = this.selectedTask.id;
    this.task.title = this.selectedTask.title;
    this.task.body = this.selectedTask.body;
    this.task.priority = this.selectedTask.priority;
    this.task.is_done = this.selectedTask.is_done;
  },
  methods: {
    edit() {
      this.$emit('edit', this.task);
    },
  }

};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

.my-input {
  min-width: 300px;
  min-height: 30px;
  margin-top: 10px;
  padding: 10px;
}
</style>