<template>
  <div class="error-message">
    <p>{{ message }}</p>
  </div>
</template>

<script setup>
const props = defineProps({
  message: String,
});
</script>

<style scoped>
.error-message {
  color: red;
  font-weight: bold;
}
</style>
