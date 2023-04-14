<script setup>

import { ref, computed, onUnmounted, onMounted } from 'vue'

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoaderSpinner from './components/LoaderSpinner.vue';

const cargandoPosts = ref(false);

const posts = ref([]);
const postPorPagina = 10;
const inicio = ref(0);
const fin = ref(postPorPagina);
const favorito = ref('ninguno');
const totalPosts = computed(() => posts.value.length);

const miPostFavorito = (title) => favorito.value = title;

const nextPaginacion = () => {
  inicio.value = inicio.value + postPorPagina;
  fin.value = fin.value + postPorPagina;
}

const prevPaginacion = () => {
  inicio.value = inicio.value - postPorPagina;
  fin.value = fin.value - postPorPagina;
}
// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then(res => res.json())
//   .then(data => posts.value = data)
//   .finally(() =>
//     setTimeout(() => {
//       cargandoPosts.value = false
//     }, 1000
//     )
//   )

// termina de mostrar el html
onMounted(async () => {
  cargandoPosts.value = true
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await response.json();

  } catch (error) {
    alert(error);
  } finally {
    setTimeout(() => {
      cargandoPosts.value = false
    }, 1000);
  }

})

</script>

<template>
  <LoaderSpinner v-if="cargandoPosts" />

  <div class="container-sm" v-else>
    <h1> App </h1>
    <h2> Mis post favorito: <u>{{ favorito }}</u> </h2>

    <div class="bg-light my-3 p-1 rounded-3 text-center text-lg-end">
      <PaginatePost :inicio="inicio" :fin="fin" :total="totalPosts" v-on:prevPaginacion="prevPaginacion"
        v-on:nextPaginacion="nextPaginacion" />
    </div>
    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-2 g-lg-5">
      <div v-for="post in posts.slice(inicio, fin)" class="col">
        <BlogPost :key="post.id" :id="post.id" :title="post.title" :body="post.body" v-on:miPostFavorito="miPostFavorito" />
      </div>

    </div>

  </div>
</template>

<style></style>

