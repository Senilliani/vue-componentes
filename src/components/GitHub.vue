<script setup>
import GitHubRepo from './GitHubRepo.vue';
import { ref } from 'vue';

// variables reactivas de datos 
const nombre = ref('');
const error = ref(false);
const mostrarDatos = ref(false);
const mostrarListado = ref(false);
const datosUsuario = ref({});
const repositorios = ref([]);
const buscando = ref(false);

const obtenerUsuario = (event) => {
  if (event.key === 'Enter') {
    console.log(nombre.value);
    buscando.value = true;
    // fetch 
    
    buscando.value = false;
  }
}

</script>

<template>
  <div class="row">
    <div class="col-10 col-lg-6  col-md-6 m-auto mt-4">
      <input type="text" class="form-control" placeholder="Introduzca nombre de usuario"
      @keydown="obtenerUsuario" v-model="nombre" :disabled="buscando">
    </div>
  </div>

  <div class="text-danger text-center mt-4" v-if="error">
    El usuario {{ nombre }} no existe.
  </div>

<!-- Capa para mostrar los datos del usuario -->
  <div class="text-center bg-body-tertiary rounded-3 mt-4 py-4" v-if="mostrarDatos">
    <img width="100" height="100">
    <h1 class="text-body-emphasis">El login del usuario</h1>
    <p class="col-lg-8 mx-auto fs-5 text-muted">
      Un enlace a la URL de GitHub del usuario
    </p>
    <div class="d-inline-flex gap-2 mb-5">
      <button @click="obtenerRepositorios" class="d-inline-flex align-items-center btn btn-primary btn-lg px-4 rounded-pill" type="button">
        Repositorios
      </button>
      <button class="btn btn-outline-secondary btn-lg px-4 rounded-pill" type="button">
        Secondary link
      </button>
    </div>
  </div>

  <!-- Capa para mostrar la lista de repositorios del usuario -->
  <div class="row" v-if="mostrarListado">
    <GitHubRepo class="col-6" v-for="repositorio in repositorios" :key="repositorio" :repo="repositorio"/> <!-- For each  v-for="repo in repositorios" ??-->
  </div>
</template>

<style scoped></style>
