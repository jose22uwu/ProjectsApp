<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import { useRoute } from 'vue-router'
import { useProyectosStore } from '@/stores/proyectos'
import type { Tarea } from '@/stores/proyectos'
import ProgressBar from '@/components/menu/ProgressBar.vue'

const route = useRoute()
const store = useProyectosStore()
const nuevaTarea = ref('')
const inputRef = ref<HTMLInputElement | null>(null)

const proyecto = computed(() => {
  const id = Number(route.params.id)
  return store.proyectos.find(p => p.id === id)
})

const agregarTarea = () => {
  if (nuevaTarea.value.trim() && proyecto.value) {
    store.agregarTarea(proyecto.value.id, nuevaTarea.value.trim())
    nuevaTarea.value = ''
  }
}

const toggleTarea = (tareaId: number) => {
  if (proyecto.value) {
    store.toggleTarea(proyecto.value.id, tareaId)
  }
}

onMounted(() => {
  inputRef.value?.focus()
})
</script>

<template>
  <div class="p-6">
    <div v-if="proyecto" class="space-y-6">
      <h1 class="text-2xl font-bold">{{ proyecto.nombre }}</h1>
      
      <!-- Tabla de tareas -->
      <div class="overflow-x-auto">
        <table class="table w-full">
          <thead>
            <tr>
              <th>#</th>
              <th>Nombre</th>
              <th>Completado</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="tarea in proyecto.tareas" :key="tarea.id">
              <td>{{ tarea.id }}</td>
              <td>{{ tarea.nombre }}</td>
              <td>
                <input
                  type="checkbox"
                  :checked="tarea.completada"
                  @change="toggleTarea(tarea.id)"
                  class="checkbox"
                />
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Formulario para nueva tarea -->
      <div class="flex gap-2">
        <input
          v-model="nuevaTarea"
          type="text"
          placeholder="Nueva tarea"
          class="input input-bordered input-sm w-1/3"
          @keydown.enter.prevent="agregarTarea"
          ref="inputRef"
        />
        <button
          class="btn btn-primary"
          @click="agregarTarea"
          :disabled="!nuevaTarea.trim()"
        >
          Agregar
        </button>
      </div>

      <button @click="$router.push('/')" class="btn btn-outline btn-sm mt-4">← Volver a proyectos</button>
    </div>
    <div v-else class="text-center text-gray-500">
      Proyecto no encontrado
    </div>
  </div>
</template> 