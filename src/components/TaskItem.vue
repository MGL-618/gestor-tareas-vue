<script setup>
import { computed } from 'vue'

const props = defineProps({
  task: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['toggle', 'edit', 'delete'])

const fechaFormateada = computed(() => {
  if (!props.task.fechaLimite) return ''
  const fecha = new Date(`${props.task.fechaLimite}T00:00:00`)
  return new Intl.DateTimeFormat('es-MX', {
    day: 'numeric',
    month: 'short',
    year: 'numeric',
  }).format(fecha)
})

const vencida = computed(() => {
  if (!props.task.fechaLimite || props.task.completada) return false
  const hoy = new Date()
  hoy.setHours(0, 0, 0, 0)
  return new Date(`${props.task.fechaLimite}T00:00:00`) < hoy
})
</script>

<template>
  <article class="task-card" :class="{ 'task-card-done': task.completada }">
    <button
      class="task-check"
      :class="{ checked: task.completada }"
      type="button"
      :aria-label="task.completada ? 'Marcar como pendiente' : 'Marcar como completada'"
      :aria-pressed="task.completada"
      @click="emit('toggle', task.id)"
    >
      <span v-if="task.completada" aria-hidden="true">✓</span>
    </button>

    <div class="task-main">
      <div class="task-title-row">
        <h3 :class="{ 'completed-title': task.completada }">{{ task.titulo }}</h3>
        <span class="priority-badge" :class="`priority-${task.prioridad.toLowerCase()}`">
          {{ task.prioridad }}
        </span>
      </div>
      <p class="task-subject">{{ task.materia }}</p>
      <p v-if="fechaFormateada" class="task-due" :class="{ overdue: vencida }">
        <span aria-hidden="true">◷</span>
        {{ vencida ? 'Vencida: ' : 'Fecha límite: ' }}{{ fechaFormateada }}
      </p>
      <span v-if="task.completada" class="completed-label">Completada</span>
    </div>

    <div class="task-actions">
      <button class="icon-button" type="button" :aria-label="`Editar ${task.titulo}`" title="Editar" @click="emit('edit', task)">
        <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 20h9"/><path d="M16.5 3.5a2.12 2.12 0 0 1 3 3L8 18l-4 1 1-4Z"/></svg>
      </button>
      <button class="icon-button danger-action" type="button" :aria-label="`Eliminar ${task.titulo}`" title="Eliminar" @click="emit('delete', task.id)">
        <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M3 6h18"/><path d="M8 6V4h8v2"/><path d="m19 6-1 14H6L5 6"/><path d="M10 11v5M14 11v5"/></svg>
      </button>
    </div>
  </article>
</template>
