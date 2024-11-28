<template>
  <div>
    <h1>{{ title }}</h1>
    <ErrorMessage v-if="error" :message="error" />

    <Todolist
      :todos="firstTenTodo"
      @toggleState="toggleState"
      @deleteItem="deleteItem"
    />

    <AddItem @addItem="addItem" />
    <SortButton @sortData="sortData" :isSorted="isSorted" />
  </div>
</template>

<script>
import { defineComponent } from "vue";
import Todolist from "./components/Todolist.vue";
import AddItem from "./components/AddItem.vue";
import ErrorMessage from "./components/ErrorMessage.vue";
import SortButton from "./components/SortButton.vue";

export default defineComponent({
  components: {
    Todolist,
    AddItem,
    ErrorMessage,
    SortButton,
  },
  data() {
    return {
      title: "Todolist",
      newEntry: "",
      todolist: [],
      firstTenTodo: [],
      isSorted: false,
      error: null,
    };
  },
  methods: {
    async getTodolist() {
      this.todolist = null;
      this.firstTenTodo = null;
      this.error = null;

      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/todos"
        );
        if (!response.ok) {
          throw new Error(`HTTP Error Status : ${response.status}`);
        }
        const result = await response.json();
        this.todolist = result;
        this.firstTenTodo = result.slice(0, 10);
      } catch (err) {
        this.error = `An error occurred while retrieving data : ${err.message}. Please try again.`;
      }
    },
    toggleState(todo) {
      todo.completed = !todo.completed;
    },
    addItem(newEntry) {
      if (/\d/.test(newEntry)) {
        alert("We cannot add this task, because it contains a number");
      } else if (newEntry === "") {
        alert("We cannot add this task, because it is void");
      } else {
        this.firstTenTodo.push({
          userId: 1,
          id: this.firstTenTodo.length + 1,
          title: newEntry,
          completed: false,
        });
      }
    },
    deleteItem(id) {
      this.firstTenTodo.splice(id, 1);
    },
    sortData() {
      this.isSorted = !this.isSorted;
      if (this.isSorted) {
        this.firstTenTodo = [...this.firstTenTodo].sort(
          (a, b) => b.completed - a.completed
        );
      } else {
        this.firstTenTodo = [...this.firstTenTodo].sort((a, b) => a.id - b.id);
      }
    },
  },
  mounted() {
    this.getTodolist();
  },
});
</script>

<style scoped>
h1 {
  color: #111;
  text-align: center;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
</style>
