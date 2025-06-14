<script setup lang="ts">
import { ref } from 'vue'
const modalRef = ref<HTMLDialogElement | null>(null)
const emit = defineEmits(['guardar'])
const openModal = () => modalRef.value?.showModal()
const closeModal = () => modalRef.value?.close()
defineExpose({ openModal, closeModal })
</script>

<template>
  <div>
    <button
      @click="openModal"
      class="btn btn-circle btn-primary"
      aria-label="Abrir modal"
    >
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 6.75A2.25 2.25 0 0 1 4.5 4.5h3.379a2.25 2.25 0 0 1 1.591.659l1.621 1.621a.75.75 0 0 0 .53.22h6.879a2.25 2.25 0 0 1 2.25 2.25v7.5a2.25 2.25 0 0 1-2.25 2.25h-15A2.25 2.25 0 0 1 2.25 16.5v-9.75z" />
        <path stroke-linecap="round" stroke-linejoin="round" d="M12 11.25v3m0 0v-3m0 0h3m-3 0h-3" />
      </svg>
    </button>
    <dialog ref="modalRef" class="modal">
      <div class="modal-box">
        <slot
          :close="closeModal"
          :guardar="(texto: string) => { emit('guardar', texto); closeModal() }"
        />
      </div>
    </dialog>
  </div>
</template>


