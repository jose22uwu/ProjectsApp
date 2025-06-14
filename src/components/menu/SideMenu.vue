<script setup lang="ts">
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import AddButtonMenu2 from '@/components/menu/AddButtonMenu2.vue'
import { useProyectosStore } from '@/stores/proyectos'

const store = useProyectosStore()
const router = useRouter()
const route = useRoute()
const nuevoProyecto = ref('')
const abiertos = ref<number[]>([])

const irAProyecto = (id: number) => {
  router.push(`/proyecto/${id}`)
}

const toggleProyecto = (id: number) => {
  if (abiertos.value.includes(id)) {
    abiertos.value = abiertos.value.filter(pid => pid !== id)
  } else {
    abiertos.value.push(id)
  }
}
</script>

<template>
  <div class="relative min-h-screen p-6">
    <ul
      v-if="store.proyectos.length > 0"
      class="menu bg-base-200 rounded-box w-56 mb-4"
    >
      <li v-for="proyecto in store.proyectos" :key="proyecto.id" class="flex flex-col">
        <div class="flex items-center justify-between">
          <span @click="toggleProyecto(proyecto.id)" class="cursor-pointer select-none text-lg mr-1">
            <span v-if="abiertos.includes(proyecto.id)">▲</span>
            <span v-else>▼</span>
          </span>
          <a @click="irAProyecto(proyecto.id)" class="cursor-pointer flex-1 hover:underline">
            {{ proyecto.nombre }}
          </a>
        </div>
        <ul v-if="abiertos.includes(proyecto.id) && proyecto.tareas.length > 0" class="ml-6 mt-1">
          <li v-for="tarea in proyecto.tareas" :key="tarea.id" class="text-sm text-gray-600">
            - {{ tarea.nombre }}
          </li>
        </ul>
      </li>
    </ul>

    <p v-else class="text-center text-gray-500 italic">
      No existen proyectos
    </p>

    <AddButtonMenu2 v-if="route.name === 'home' || route.name === 'proyectos'" @guardar="(nuevo: string) => { store.agregarProyecto(nuevo) }">
      <template #default="{ guardar, close }">
        <h3 class="font-bold text-lg">Agregue proyectos aquí</h3>
        <input
          v-model="nuevoProyecto"
          type="text"
          placeholder="Nombre del proyecto"
          class="input input-bordered w-full my-4"
          @keydown.enter.prevent="
            nuevoProyecto.trim() !== '' && (
              guardar(nuevoProyecto.trim()), 
              nuevoProyecto = ''
            )
          "
        />
        <div class="modal-action flex justify-between">
          <button
            class="btn btn-primary w-1/2 mr-2"
            @click="guardar(nuevoProyecto.trim()); nuevoProyecto = ''"
            :disabled="nuevoProyecto.trim() === ''"
          >
            Guardar
          </button>
          <button
            class="btn btn-primary w-1/2"
            @click="close(); nuevoProyecto = ''"
          >
            Cerrar
          </button>
        </div>
      </template>
    </AddButtonMenu2>
  </div>
</template>

<style scoped>
:deep(.btn-circle) {
  width: 3.5rem;
  height: 3.5rem;
  position: fixed;
  bottom: 1.5rem;
  left: 1.5rem;
}
</style>
