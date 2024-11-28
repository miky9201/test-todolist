<template>
  <div>
    <input v-model="newEntry" type="text" placeholder="Enter task" />
    <button @click="addItem">Add</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newEntry: "",
    };
  },
  methods: {
    addItem() {
      this.$emit("addItem", this.newEntry);
      this.newEntry = ""; // Reset input field
    },
  },
};
</script>
