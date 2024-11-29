<template>
  <li :class="{ completed: todo.completed }" class="todo">
    {{ id + 1 }} - {{ todo.title }}

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

<script setup>
const props = defineProps({
  todo: Object,
  id: Number,
});

const emit = defineEmits(["toggleState", "deleteItem"]);

const toggleState = (todo) => {
  emit("toggleState", todo);
};

const deleteItem = (id) => {
  emit("deleteItem", id);
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
.btn-done:hover {
  border: 1px solid rgb(235, 0, 125);
}

.btn-todo:hover {
  border: 1px solid rgb(45, 206, 120);
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
