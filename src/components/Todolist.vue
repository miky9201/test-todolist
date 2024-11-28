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

<script>
import { defineComponent } from "vue";
import TodoItem from "./TodoItem.vue";

export default defineComponent({
  components: {
    TodoItem,
  },
  props: {
    todos: Array,
  },
  methods: {
    toggleState(todo) {
      this.$emit("toggleState", todo);
    },
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
  },
});
</script>
<style scoped>
.todolist {
  background-color: #111;
  padding: 10px 10px;
  border-radius: 10px;
}
</style>
