<script setup>
import { computed, ref, watch } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'
import TaskStats from './components/TaskStats.vue'

const STORAGE_KEY = 'gestor-tareas-vue-tareas'

const tareasIniciales = [
  {
    id: 1,
    titulo: 'Estudiar VLSM',
    materia: 'Redes',
    prioridad: 'Alta',
    fechaLimite: '',
    completada: false,
    creadaEn: new Date().toISOString(),
  },
  {
    id: 2,
    titulo: 'Repasar componentes de Vue',
    materia: 'Programación Web',
    prioridad: 'Media',
    fechaLimite: '',
    completada: false,
    creadaEn: new Date().toISOString(),
  },
  {
    id: 3,
    titulo: 'Practicar consultas SQL',
    materia: 'Bases de Datos',
    prioridad: 'Baja',
    fechaLimite: '',
    completada: true,
    creadaEn: new Date().toISOString(),
  },
]

function cargarTareas() {
  try {
    const guardadas = localStorage.getItem(STORAGE_KEY)
    if (guardadas !== null) {
      const parseadas = JSON.parse(guardadas)
      return Array.isArray(parseadas) ? parseadas : tareasIniciales
    }
  } catch (error) {
    console.error('No se pudieron cargar las tareas guardadas:', error)
  }
  return tareasIniciales
}

const tareas = ref(cargarTareas())
const mostrarFormulario = ref(false)
const tareaEnEdicion = ref(null)
const busqueda = ref('')
const filtroEstado = ref('Todas')
const filtroPrioridad = ref('Todas')
const aviso = ref('')

watch(
  tareas,
  (nuevasTareas) => {
    try {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(nuevasTareas))
    } catch (error) {
      console.error('No se pudieron guardar las tareas:', error)
      aviso.value = 'No fue posible guardar los cambios en este navegador.'
    }
  },
  { deep: true },
)

const tareasFiltradas = computed(() => {
  const texto = busqueda.value.trim().toLocaleLowerCase('es')

  return tareas.value.filter((tarea) => {
    const coincideTexto =
      !texto ||
      tarea.titulo.toLocaleLowerCase('es').includes(texto) ||
      tarea.materia.toLocaleLowerCase('es').includes(texto)

    const coincideEstado =
      filtroEstado.value === 'Todas' ||
      (filtroEstado.value === 'Pendientes' && !tarea.completada) ||
      (filtroEstado.value === 'Completadas' && tarea.completada)

    const coincidePrioridad =
      filtroPrioridad.value === 'Todas' || tarea.prioridad === filtroPrioridad.value

    return coincideTexto && coincideEstado && coincidePrioridad
  })
})

const estadisticas = computed(() => {
  const total = tareas.value.length
  const completadas = tareas.value.filter((tarea) => tarea.completada).length
  const pendientes = total - completadas
  const hoy = new Date()
  hoy.setHours(0, 0, 0, 0)
  const vencidas = tareas.value.filter((tarea) => {
    if (!tarea.fechaLimite || tarea.completada) return false
    return new Date(`${tarea.fechaLimite}T00:00:00`) < hoy
  }).length

  return { total, completadas, pendientes, vencidas }
})

function abrirFormularioNuevo() {
  tareaEnEdicion.value = null
  mostrarFormulario.value = true
  aviso.value = ''
}

function abrirEdicion(tarea) {
  tareaEnEdicion.value = { ...tarea }
  mostrarFormulario.value = true
  aviso.value = ''
}

function guardarTarea(datos) {
  if (tareaEnEdicion.value) {
    tareas.value = tareas.value.map((tarea) =>
      tarea.id === tareaEnEdicion.value.id ? { ...tarea, ...datos } : tarea,
    )
    aviso.value = 'Tarea actualizada.'
  } else {
    tareas.value.unshift({
      ...datos,
      id: Date.now(),
      completada: false,
      creadaEn: new Date().toISOString(),
    })
    aviso.value = 'Tarea agregada.'
  }
  mostrarFormulario.value = false
  tareaEnEdicion.value = null
}

function cambiarEstado(id) {
  tareas.value = tareas.value.map((tarea) =>
    tarea.id === id ? { ...tarea, completada: !tarea.completada } : tarea,
  )
}

function eliminarTarea(id) {
  const tarea = tareas.value.find((item) => item.id === id)
  if (!tarea) return
  const confirmar = window.confirm(`¿Quieres eliminar la tarea "${tarea.titulo}"?`)
  if (!confirmar) return
  tareas.value = tareas.value.filter((item) => item.id !== id)
  aviso.value = 'Tarea eliminada.'
}

function cancelarFormulario() {
  mostrarFormulario.value = false
  tareaEnEdicion.value = null
}

function limpiarFiltros() {
  busqueda.value = ''
  filtroEstado.value = 'Todas'
  filtroPrioridad.value = 'Todas'
}
</script>

<template>
  <div class="app-shell">
    <header class="topbar">
      <a class="brand" href="#inicio" aria-label="Gestor de tareas, inicio">
        <span class="brand-mark" aria-hidden="true">GT</span>
        <span>Organiza tu semestre</span>
      </a>
      <span class="topbar-note">Tu espacio académico</span>
    </header>

    <main id="inicio" class="main-content">
      <section class="hero">
        <div class="hero-copy">
          <p class="eyebrow">PLANIFICA · AVANZA · CUMPLE</p>
          <h1>Gestor de tareas</h1>
          <p class="hero-description">
            Ten tus actividades académicas en orden y concéntrate en lo que sigue.
          </p>
        </div>
        <button class="button button-primary hero-button" type="button" @click="abrirFormularioNuevo">
          <span aria-hidden="true">＋</span> Nueva tarea
        </button>
      </section>

      <TaskStats
        :total="estadisticas.total"
        :completadas="estadisticas.completadas"
        :pendientes="estadisticas.pendientes"
        :vencidas="estadisticas.vencidas"
      />

      <section v-if="mostrarFormulario" class="panel form-panel" aria-labelledby="form-title">
        <div class="panel-heading">
          <div>
            <p class="eyebrow">DETALLES DE LA ACTIVIDAD</p>
            <h2 id="form-title">{{ tareaEnEdicion ? 'Editar tarea' : 'Crear una tarea' }}</h2>
          </div>
          <button class="icon-button" type="button" aria-label="Cerrar formulario" @click="cancelarFormulario">×</button>
        </div>
        <TaskForm
          :initial-task="tareaEnEdicion"
          @save="guardarTarea"
          @cancel="cancelarFormulario"
        />
      </section>

      <section class="panel tasks-panel" aria-labelledby="tasks-title">
        <div class="panel-heading task-heading">
          <div>
            <p class="eyebrow">TU PLAN DE TRABAJO</p>
            <h2 id="tasks-title">Mis tareas <span class="count-pill">{{ tareasFiltradas.length }}</span></h2>
          </div>
          <button class="button button-secondary desktop-add" type="button" @click="abrirFormularioNuevo">
            ＋ Agregar tarea
          </button>
        </div>

        <div class="filters">
          <label class="search-box">
            <span class="sr-only">Buscar por tarea o materia</span>
            <span class="search-icon" aria-hidden="true">⌕</span>
            <input v-model="busqueda" type="search" placeholder="Buscar tarea o materia..." />
          </label>
          <label class="filter-field">
            <span>Estado</span>
            <select v-model="filtroEstado">
              <option>Todas</option>
              <option>Pendientes</option>
              <option>Completadas</option>
            </select>
          </label>
          <label class="filter-field">
            <span>Prioridad</span>
            <select v-model="filtroPrioridad">
              <option>Todas</option>
              <option>Alta</option>
              <option>Media</option>
              <option>Baja</option>
            </select>
          </label>
        </div>

        <p v-if="aviso" class="notice" role="status">{{ aviso }}</p>

        <TaskList
          :tasks="tareasFiltradas"
          :has-any-tasks="tareas.length > 0"
          @toggle="cambiarEstado"
          @edit="abrirEdicion"
          @delete="eliminarTarea"
        />

        <div v-if="tareas.length && tareasFiltradas.length === 0" class="filter-empty">
          <p>No encontramos tareas con esos filtros.</p>
          <button class="text-button" type="button" @click="limpiarFiltros">Limpiar filtros</button>
        </div>
      </section>

      <p class="privacy-note">
        Tus tareas se guardan en el almacenamiento local de este navegador. No necesitas crear una cuenta.
      </p>
    </main>

    <footer class="footer">
      <span>Gestor de tareas académicas</span>
      <span>Hecho para organizar mejor tu tiempo</span>
    </footer>
  </div>
</template>
