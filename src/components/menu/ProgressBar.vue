<script setup lang="ts">
defineProps<{
  value: number
  max?: number
}>()
</script>

<template>
  <progress 
    class="progress progress-info w-56" 
    :value="value" 
    :max="max || 100"
  ></progress>
</template> 