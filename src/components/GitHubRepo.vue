<script setup>
// Lo que acepta
defineProps({
   repo: Object
})
</script>

<template>
  <div class="list-group">
    <a href="#" class="list-group-item list-group-item-action d-flex gap-3 py-3 mt-4" aria-current="true">
      <img src="https://github.com/twbs.png" alt="twbs" width="32" height="32" class="rounded-circle flex-shrink-0">
      <div class="d-flex gap-2 w-100 justify-content-between">
        <div>
          <h6 class="mb-0">{{ repo }}</h6>
          <p class="mb-0 opacity-75">Some placeholder content in a paragraph.</p>
        </div>
        <small class="opacity-50 text-nowrap">now</small>
      </div>
    </a>
  </div>
</template>

<style scoped></style>
