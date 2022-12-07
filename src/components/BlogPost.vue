<script setup>
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: "sin descripcion",
  },
  cambiarFavorito: Function,
});

// tambien podemos definir los emits
// const llamarEmit = defineEmits(["cambiarFavoritoNombre"]);
</script>

<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ id }} - {{ title }}</h5>
      <P>{{ body }}</P>
      <!-- <button
        @click="$emit('cambiarFavoritoNombre', title)"
        class="btn btn-outline-primary"
      >
        Favorito
      </button> -->
      <button @click="cambiarFavorito(title)" class="btn btn-outline-primary">
        Favorito
      </button>
    </div>
  </div>
</template>

<style></style>
