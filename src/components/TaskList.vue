<template>
  <div v-if="tasks.length > 0">
    <h3>Список задач</h3>
    <task-item 
      v-for="task in tasks" 
      :task="task" 
      :key="task.id"
      @showEditDialog="$emit('showEditDialog', task)"
      @remove="$emit('remove', task)"
    />
  </div>
  <h3 v-else>Список пуст</h3>
</template>

<script>
import TaskItem from "@/components/TaskItem";
export default {
  components: { TaskItem },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
</style>