<script setup>
import GitHubRepo from './GitHubRepo.vue';
import { ref } from 'vue';

// variables reactivas de datos 
const nombre = ref('');
const error = ref(false);
const mostrarDatos = ref(false);
const mostrarRepositorios = ref(false);
const datosUsuario = ref({});
const datosRepositorio = ref([]);
const buscando = ref(false);

const limpiarDatos = () => {
  error.value = false;
  mostrarDatos.value = false;
  mostrarRepositorios.value = false;
}

const obtenerUsuario = async (event) => {
  limpiarDatos();
  if (event.key === 'Enter') {
    buscando.value = true;
    try {
      const url = `https://api.github.com/users/${nombre.value}`;
      const respuesta = await fetch(url);
      if (respuesta.ok) {
        datosUsuario.value = await respuesta.json();
        nombre.value = datosUsuario.value.login;
        mostrarDatos.value = true;
      }
      else {
        throw new Error();
      }
    }
    catch {
      error.value = true;
    }
    buscando.value = false;
  }
}

const obtenerRepositorios = async () => {
  try {
    const url = datosUsuario.value.repos_url;
    const respuesta = await fetch(url);

    if (respuesta.ok) {
      datosRepositorio.value = await respuesta.json();
      mostrarRepositorios.value = true;
    }
    else {
      throw new Error();
    }
  }
  catch {
    alert('Error al obtener los repositorios');
  }
}

</script>

<template>
  <div class="row">
    <div class="col-10 col-lg-6  col-md-6 m-auto mt-4">
      <input type="text" class="form-control" placeholder="Introduzca nombre de usuario" @keydown="obtenerUsuario"
        v-model="nombre" :disabled="buscando">
    </div>
  </div>

  <div class="text-danger text-center mt-4" v-if="error">
    El usuario {{ nombre }} no existe.
  </div>

  <!-- Capa para mostrar los datos del usuario -->
  <div class="text-center bg-body-tertiary rounded-3 mt-4 py-4" v-if="mostrarDatos">
    <img width="150" height="150" class="rounded-circle" :src="datosUsuario.avatar_url">
    <h1 class="text-body-emphasis"> {{ datosUsuario.login }} </h1>
    <div class="d-inline-flex gap-2">
      <button @click="obtenerRepositorios"
        class="d-inline-flex align-items-center btn btn-primary btn-lg px-4 rounded-pill" type="button">
        Repositorios
      </button>
      <a :href="datosUsuario.html_url" target="_blank" class="btn btn-outline-secondary btn-lg px-4 rounded-pill"
        type="button">
        URL de GitHub
      </a>
    </div>
  </div>

  <!-- Capa para mostrar la lista de repositorios del usuario -->
  <div class="row mb-5" v-if="mostrarRepositorios">
    <GitHubRepo v-for="repositorio in datosRepositorio" :key="repositorio.id" :repo="repositorio" />
  </div>
</template>

<style scoped></style>
