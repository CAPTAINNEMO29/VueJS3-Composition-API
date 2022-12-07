<script setup>
defineProps(["inicio", "fin", "maxPosts"]);
const emit = defineEmits(["next", "prev"]);
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      @click="emit('prev')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="inicio === 0"
    >
      Previous
    </button>
    <button
      @click="emit('next')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="fin >= maxPosts"
    >
      Next
    </button>
  </div>
</template>
