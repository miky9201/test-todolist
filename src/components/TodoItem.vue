<template>
  <li :class="{ completed: todo.completed }" class="todo">
    {{ todo.id }} - {{ todo.title }}

    <button v-if="todo.completed" class="btn" @click="toggleState(todo)">
      Done
    </button>
    <button v-else class="btn" @click="toggleState(todo)">To Do</button>
    <button class="btn" @click="deleteItem(id)">X</button>

    <img v-if="todo.completed === true" src="../assets/done.png" width="15px" />
  </li>
</template>

<script>
export default {
  props: {
    todo: Object,
    id: Number,
  },
  methods: {
    toggleState(todo) {
      this.$emit("toggleState", todo);
    },
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
  },
};
</script>
<style scoped>
li {
  color: red;
  list-style: none;
}

.completed {
  color: green;
}
</style>
