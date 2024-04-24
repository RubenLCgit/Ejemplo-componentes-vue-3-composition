<script setup>

  defineProps({
    statePrevius: Boolean,
    stateNext: Boolean
  });

  const emit = defineEmits(['nextPost', 'previusPost']);

</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button @click="emit('previusPost')" type="button" class="btn btn-primary" :disabled="statePrevius">Previus</button>
    <button @click="emit('nextPost')" type="button" class="btn btn-secondary" :disabled="stateNext">Next</button>
  </div>
</template>

<style scoped>

button {
  max-width: 100px;
}

.btn-group {
  display: flex;
  justify-content: center;
}

</style>