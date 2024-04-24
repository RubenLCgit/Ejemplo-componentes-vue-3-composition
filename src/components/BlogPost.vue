<script setup>
  const props = defineProps({
    title: String,
    id: Number,
    body: {String, default: 'Sin descripción'},
    colorText: String
  });

  const emit = defineEmits(['cambiarNombreFavorito']);

</script>

<template>
  <div class="card">
    <div class="card__body">
      <h5 :id="id" class="card__title" :class="`text-${colorText}`">{{ title }}</h5>
      <p>{{body}}</p>
      <button @click="emit('cambiarNombreFavorito', title)" class="btn btn-outline-primary">Favorito</button>
    </div>
  </div>
</template>

<style scoped>
  h1 {
    color: red;
  }
</style>