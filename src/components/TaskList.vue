<script setup>
import TaskItem from './TaskItem.vue'

defineProps({
  tasks: {
    type: Array,
    required: true,
  },
  hasAnyTasks: {
    type: Boolean,
    default: true,
  },
})

const emit = defineEmits(['toggle', 'edit', 'delete'])
</script>

<template>
  <div v-if="tasks.length" class="task-list">
    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @toggle="emit('toggle', $event)"
      @edit="emit('edit', $event)"
      @delete="emit('delete', $event)"
    />
  </div>
  <div v-else-if="!hasAnyTasks" class="empty-state">
    <span class="empty-icon" aria-hidden="true">✓</span>
    <h3>Todo en orden</h3>
    <p>No hay tareas pendientes en esta vista. Puedes agregar una nueva cuando quieras.</p>
  </div>
</template>
