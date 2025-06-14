<script setup lang="ts">
import Top from '@/components/menu/TopMenu.vue'
import Side from '@/components/menu/SideMenu.vue'
import { RouterView, useRoute } from 'vue-router'

const route = useRoute()
</script>

<template>
  <div class="flex flex-col h-screen">
    <!-- Header -->
    <Top />

    <!-- Contenedor principal -->
    <div class="flex flex-1 overflow-hidden">
      <!-- Sidebar a la izquierda -->
      <Side />

      <!-- Contenedor de contenido + botón -->
      <div class="flex-1 relative overflow-auto p-6 ml-8">
        <!-- Contenido principal -->
        <RouterView />

        <!-- Botón flotante eliminado -->
      </div>
    </div>
  </div>
</template>
