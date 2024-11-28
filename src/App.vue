<script>
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      title: "Todolist",
    };
  },
  methods: {},
});
</script>

<template>
  <h1>{{ title }}</h1>
  <ul>
    <li>Todo 1</li>
    <li>Todo 2</li>
    <li>Todo 3</li>
  </ul>
</template>

<style scoped>
h1 {
  color: #111;
}
</style>
