<template>
  <button class="btn btn-sort" @click="sortData">
    {{ isSorted ? "Revert Sort" : "Sort by Done" }}
  </button>
</template>

<script setup>
const props = defineProps({
  isSorted: Boolean,
});

const emit = defineEmits(["sortData"]);

const sortData = () => {
  emit("sortData");
};
</script>

<style scoped>
.btn-sort {
  text-align: center;
}
</style>
