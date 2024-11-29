<template>
  <h1>{{ title }}</h1>
  <ErrorMessage v-if="error" :message="error" />
  <SortButton @sortData="sortData" :isSorted="isSorted" />

  <Todolist
    :todos="firstTenTodo"
    @toggleState="toggleState"
    @deleteItem="deleteItem"
  />

  <AddItem @addItem="addItem" />
</template>

<script setup>
import { ref, onMounted } from "vue";
import Todolist from "./components/Todolist.vue";
import AddItem from "./components/AddItem.vue";
import ErrorMessage from "./components/ErrorMessage.vue";
import SortButton from "./components/SortButton.vue";

const title = ref("Todolist");
const newEntry = ref("");
const todolist = ref([]);
const firstTenTodo = ref([]);
const isSorted = ref(false);
const error = ref(null);

const getTodolist = async () => {
  todolist.value = null;
  firstTenTodo.value = null;
  error.value = null;

  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    if (!response.ok) {
      throw new Error(`HTTP Error Status : ${response.status}`);
    }
    const result = await response.json();
    todolist.value = result;
    firstTenTodo.value = result.slice(0, 10);
  } catch (err) {
    error.value = `An error occurred while retrieving data : ${err.message}. Please try again.`;
  }
};

const toggleState = (todo) => {
  todo.completed = !todo.completed;
};

const addItem = (newEntryValue) => {
  if (/\d/.test(newEntryValue)) {
    alert("We cannot add this task, because it contains a number");
  } else if (newEntryValue === "") {
    alert("We cannot add this task, because it is void");
  } else {
    firstTenTodo.value.push({
      userId: 1,
      id: firstTenTodo.value.length + 1,
      title: newEntryValue,
      completed: false,
    });
  }
};

const deleteItem = (id) => {
  firstTenTodo.value.splice(id, 1);
};

const sortData = () => {
  isSorted.value = !isSorted.value;
  if (isSorted.value) {
    firstTenTodo.value = [...firstTenTodo.value].sort(
      (a, b) => b.completed - a.completed
    );
  } else {
    firstTenTodo.value = [...firstTenTodo.value].sort((a, b) => a.id - b.id);
  }
};

onMounted(() => {
  getTodolist();
});
</script>

<style>
h1 {
  color: #111;
  text-align: center;
}

body {
  font-family: "Trebuchet MS", sans-serif;
}

.btn {
  background-color: #fff;
  border: 1px solid #d5d9d9;
  box-sizing: border-box;
  color: #0f1111;
  padding: 4px;
  color: white;
  background-color: #111;
}
</style>
