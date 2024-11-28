<template>
  <button @click="sortData">
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
