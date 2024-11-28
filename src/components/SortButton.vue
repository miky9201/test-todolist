<template>
  <button class="btn btn-sort" @click="sortData">
    {{ isSorted ? "Revert Sort" : "Sort by Done" }}
  </button>
</template>

<script>
export default {
  props: {
    isSorted: Boolean,
  },
  methods: {
    sortData() {
      this.$emit("sortData");
    },
  },
};
</script>
<style scoped>
.btn-sort {
  text-align: center;
}
</style>
