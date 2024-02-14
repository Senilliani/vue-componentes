<script setup>
// Lo que acepta
defineProps({
  repo: Object
})
</script>

<template>
  <div class="list-group px-0 col-11 m-auto col-md-5 mt-0 mx-auto">
    <div class="list-group-item list-group-item-action mt-4">
      <div class="d-flex py-3 justify-content-between align-items-center">
        <a :href="repo.html_url" target="_blank" class="fw-bold" :title="repo.description">
          {{ repo.full_name }}
        </a>
        <small class="opacity-50 text-nowrap badge bg-secondary">{{ repo.forks_count }}</small>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
