<template>
  <div class="input-container">
    <input
      class="text-entry"
      v-model="newEntry"
      type="text"
      placeholder="Enter New Todo"
    />
    <button class="btn btn-add" @click="addItem">Add</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const newEntry = ref("");

const emit = defineEmits(["addItem"]);

const addItem = () => {
  emit("addItem", newEntry.value);
  newEntry.value = "";
};
</script>

<style scoped>
.input-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.text-entry {
  text-align: center;
  padding: 12px 6px;
  margin-top: 5px;
  background: rgb(31, 32, 35);
  border: 3px solid rgb(60, 63, 68);
  border-radius: 4px;
  font-size: 13px;
  color: rgb(247, 248, 248);

  appearance: none;
  transition: border 0.15s ease 0s;
}
.text-entry:focus {
  outline: none;
  box-shadow: none;
  border-color: rgb(255, 100, 190);
}

.btn-add {
  margin-top: 5px;
}
</style>
