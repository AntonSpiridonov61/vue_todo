<template>
  <form @submit.prevent>
    <h4>Добавить задачу</h4>
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
    <my-button class="btn_form" @click="createTask">Добавить</my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      task: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createTask() {
      this.task.id = Date.now();
      this.$emit("create", this.task);
      this.task = {
        title: "",
        body: "",
      };
    },
  },
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

.btn_form {
  align-self: flex-end;
  margin-top: 15px;
}
</style>