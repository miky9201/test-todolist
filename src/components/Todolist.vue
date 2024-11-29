<template>
  <ul class="todolist">
    <TodoItem
      v-for="(todo, id) in todos"
      :key="todo.id"
      :todo="todo"
      :id="id"
      @toggleState="toggleState"
      @deleteItem="deleteItem"
    />
  </ul>
</template>

<script setup>
import TodoItem from "./TodoItem.vue";

const props = defineProps({
  todos: Array,
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
.todolist {
  background-color: #111;
  padding: 10px 10px;
  border-radius: 10px;
}
</style>
