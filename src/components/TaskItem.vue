<template>
  <div class="task">
    <div>
      <input type="checkbox" id="checkbox" v-model="is_done">
      <div><strong>Название:</strong> {{ task.title }}</div>
      <div><strong>Описание:</strong> {{ task.body }}</div>
      <div><strong>Приоритет:</strong> {{ task.priority }}</div>
    </div>
    <div>
      <div class="task_btns">
        <my-button @click="$emit('edit', task)">Редактировать</my-button>
        <my-button @click="$emit('remove', task)">Удалить</my-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.task {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task_btns {

}
</style>