<script setup>
defineProps({
  total: { type: Number, required: true },
  completadas: { type: Number, required: true },
  pendientes: { type: Number, required: true },
  vencidas: { type: Number, required: true },
})
</script>

<template>
  <section class="stats-grid" aria-label="Resumen de tareas">
    <article class="stat-card">
      <span class="stat-icon stat-icon-total" aria-hidden="true">▤</span>
      <div><p>Total de tareas</p><strong>{{ total }}</strong></div>
    </article>
    <article class="stat-card">
      <span class="stat-icon stat-icon-pending" aria-hidden="true">◷</span>
      <div><p>Pendientes</p><strong>{{ pendientes }}</strong></div>
    </article>
    <article class="stat-card">
      <span class="stat-icon stat-icon-done" aria-hidden="true">✓</span>
      <div><p>Completadas</p><strong>{{ completadas }}</strong></div>
    </article>
    <article class="stat-card">
      <span class="stat-icon stat-icon-overdue" aria-hidden="true">!</span>
      <div><p>Vencidas</p><strong>{{ vencidas }}</strong></div>
    </article>
  </section>
</template>
