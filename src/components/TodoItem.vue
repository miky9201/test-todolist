<template>
  <li :class="{ completed: todo.completed }" class="todo">
    {{ todo.id }} - {{ todo.title }}

    <button
      v-if="todo.completed"
      class="btn btn-done"
      @click="toggleState(todo)"
    >
      Done
    </button>
    <button v-else class="btn btn-todo" @click="toggleState(todo)">
      To Do
    </button>
    <button class="btn btn-delete" @click="deleteItem(id)">X</button>

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
  color: rgb(235, 0, 125);
  list-style: none;
}

.btn-done,
.btn-todo {
  margin: 5px 10px;
  padding: 5px;
  color: #fff;
  background-color: unset;
}
.btn-done:hover,
.btn-todo:hover {
  border: 3px solid rgb(224, 224, 224);
}

.btn-delete {
  padding: 4px;
  color: #fff;
  background-color: unset;
}

.completed {
  color: rgb(45, 206, 120);
}
</style>
