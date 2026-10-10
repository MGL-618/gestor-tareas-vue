<script setup>
import { reactive, watch } from 'vue'

const props = defineProps({
  initialTask: {
    type: Object,
    default: null,
  },
})

const emit = defineEmits(['save', 'cancel'])

const formulario = reactive({
  titulo: '',
  materia: '',
  prioridad: 'Media',
  fechaLimite: '',
})

function cargarFormulario(tarea) {
  formulario.titulo = tarea?.titulo ?? ''
  formulario.materia = tarea?.materia ?? ''
  formulario.prioridad = tarea?.prioridad ?? 'Media'
  formulario.fechaLimite = tarea?.fechaLimite ?? ''
}

watch(() => props.initialTask, cargarFormulario, { immediate: true })

function enviarFormulario() {
  const titulo = formulario.titulo.trim()
  const materia = formulario.materia.trim()
  if (!titulo || !materia) return

  emit('save', {
    titulo,
    materia,
    prioridad: formulario.prioridad,
    fechaLimite: formulario.fechaLimite,
  })

  if (!props.initialTask) cargarFormulario(null)
}
</script>

<template>
  <form class="task-form" @submit.prevent="enviarFormulario">
    <div class="form-grid">
      <label class="form-field form-field-wide">
        <span>Título de la tarea <span class="required">*</span></span>
        <input
          v-model="formulario.titulo"
          type="text"
          maxlength="100"
          placeholder="Ej. Entregar práctica de redes"
          required
          autofocus
        />
      </label>

      <label class="form-field">
        <span>Materia <span class="required">*</span></span>
        <input
          v-model="formulario.materia"
          type="text"
          maxlength="60"
          placeholder="Ej. Redes"
          required
        />
      </label>

      <label class="form-field">
        <span>Prioridad</span>
        <select v-model="formulario.prioridad">
          <option>Alta</option>
          <option>Media</option>
          <option>Baja</option>
        </select>
      </label>

      <label class="form-field">
        <span>Fecha límite</span>
        <input v-model="formulario.fechaLimite" type="date" />
      </label>
    </div>

    <p class="form-help"><span class="required">*</span> Campos obligatorios</p>
    <div class="form-actions">
      <button class="button button-secondary" type="button" @click="emit('cancel')">Cancelar</button>
      <button class="button button-primary" type="submit">
        {{ initialTask ? 'Guardar cambios' : 'Agregar tarea' }}
      </button>
    </div>
  </form>
</template>
