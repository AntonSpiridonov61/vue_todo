<template>
  <form @submit.prevent>
    <h4>Изменить задачу</h4>
    <input type="checkbox" v-model="task.is_done">
    <input
      v-model="task.title"
      class="input"
      type="text"
      placeholder="Название"
    />
    <input
      v-model="task.body"
      class="input"
      type="text"
      placeholder="Описание"
    />
    <my-radio v-model="task.priority" :radioOptions="radioOptions"/>
    <my-button class="btn_form" @click="edit">Сохранить</my-button>
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

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

.radio_group {
  display: flex;
  flex-direction: column;
  padding: 10px 15px;
  margin-top: 15px;
}

.radio {
  margin-top: 5px;
}

.btn_form {
  align-self: flex-end;
  margin-top: 15px;
}
</style>