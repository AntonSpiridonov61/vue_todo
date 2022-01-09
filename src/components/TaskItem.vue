<template>

  <div class="card" style="width: 100%; margin-top: 15px; z-index: 0;">
    <div class="card-body">
      <h4 class="card-title"><strong>Название: {{ task.title }}</strong></h4>
      <h6 class="card-subtitle mb-2">
        <label class="form-check-label">
          <strong>Состояние: </strong>
          <input class="form-check-input" type="checkbox" v-model="task.is_done">
        </label>
      </h6>
      <h6 class="card-subtitle mb-2"><strong>Приоритет:</strong> {{ task.priority.name }}</h6>
      <p class="card-text"><strong>Описание:</strong> {{ task.body }}</p>
      <my-button class="btn-outline-secondary" @click="$emit('showEditDialog', task)">Редактировать</my-button>
      <my-button class="btn-outline-danger" @click="$emit('remove', task)">Удалить</my-button>
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

</style>