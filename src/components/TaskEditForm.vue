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
    <my-button class="btn_form" @click="saveTask">Сохранить</my-button>
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
    selectTask: {
      type: Object,
      required: true,
    }
  },
  mounted() {
    this.task.id = this.selectTask.id;
    this.task.title = this.selectTask.title;
    this.task.body = this.selectTask.body;
    this.task.priority = this.selectTask.priority;
    this.task.is_done = this.selectTask.is_done;
  },
  methods: {
    saveTask() {
      this.$emit('saveTask', this.task);
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