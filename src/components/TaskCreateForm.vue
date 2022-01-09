<template>
  <form @submit.prevent>
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
      @click="createTask">Добавить
    </my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      task: {
        title: "",
        body: "",
        priority: {},
        is_done: false,
      },
      radioOptions: [
        {value: "1", name: "Низкий"},
        {value: "2", name: "Средний"},
        {value: "3", name: "Высокий"},
      ],
    };
  },
  methods: {
    createTask() {
      this.task.id = Date.now();
      this.$emit("create", this.task);
      this.task = {
        title: "",
        body: "",
        priority: {}
      };
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
  min-height: 40px;
  margin-top: 10px;
  padding: 10px;
}
</style>