<script setup>
defineProps({
  term: { type: String, required: true }
})
</script>

<template>
  <span class="g-term" :data-g="term">{{ term }}</span>
</template>
