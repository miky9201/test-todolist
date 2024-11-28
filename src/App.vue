<script>
import { defineComponent } from "vue";

export default defineComponent({
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
    addItem() {
      if (/\d/.test(this.newEntry)) {
        alert("We cannot add this task, because it contains a number");
      } else if (this.newEntry === "") {
        alert("We cannot add this task, because it is void");
      } else {
        this.firstTenTodo.push({
          userId: 1,
          id: this.firstTenTodo.length + 1,
          title: this.newEntry,
          completed: false,
        });
        this.newEntry = "";
      }
    },
    deleteItem(id) {
      // Supprime l'élément correspondant dans la liste des tâches
      this.firstTenTodo.splice(id, 1);
    },
    sortData() {
      this.isSorted = true;
      this.firstTenTodo = [...this.firstTenTodo].sort(
        (a, b) => b.completed - a.completed
      );
    },
  },
  mounted() {
    this.getTodolist();
  },
});
</script>

<template>
  <h1>{{ title }}</h1>
  <ul class="todolist">
    <div v-if="error" class="error-message">
      <p>{{ error }}</p>
    </div>
    <li
      :class="{ completed: todo.completed }"
      :key="todo.index"
      v-for="(todo, id) in firstTenTodo"
      class="todo"
    >
      {{ todo.id }} - {{ todo.title }}

      <button v-if="todo.completed" class="btn" @click="toggleState(todo)">
        Done
      </button>
      <button v-else class="btn" @click="toggleState(todo)">To Do</button>
      <button class="btn" @click="deleteItem(id)">X</button>

      <img
        v-if="todo.completed === true"
        src="./assets/done.png"
        width="15px"
        srcset=""
      />
    </li>
  </ul>
  <input v-model="newEntry" type="text" name="" id="" />
  <button @click="addItem">Add</button>
  <button @click="sortData">Sort by Done</button>
</template>

<style scoped>
h1 {
  color: #111;
}

li {
  color: red;
  list-style: none;
}

.completed {
  color: green;
}

.btn {
  padding: 3px;
  margin-right: 3px;
}

.error-message {
  color: red;
  font-weight: bold;
}
</style>
