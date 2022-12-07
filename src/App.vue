<script setup>
import { ref, computed, onMounted } from "vue";
import BlogPost from "./components/BlogPost.vue";
import Pagination from "./components/Pagination.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]);
const favorito = ref("");
const elementosPagina = 10;
const inicio = ref(0);
const fin = ref(elementosPagina);
const loading = ref(true);

const cambiarFavorito = (title) => {
  favorito.value = title;
};

const next = () => {
  inicio.value = inicio.value + elementosPagina;
  fin.value = fin.value + elementosPagina;
};

const prev = () => {
  inicio.value = inicio.value - elementosPagina;
  fin.value = fin.value - elementosPagina;
};

const maxPosts = computed(() => posts.value.length);

onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
        loading.value = false;
      }, 500);
  }
});


</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>App</h1>
    <h2>Mi Post Favorito {{ favorito }}</h2>
    <Pagination
      @next="next"
      @prev="prev"
      :inicio="inicio"
      :fin="fin"
      :maxPosts="maxPosts"
      class="mb-2"
    />
    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      :cambiarFavorito="cambiarFavorito"
    ></BlogPost>
  </div>
</template>

<style></style>
