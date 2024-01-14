<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        Hello, <input type="text" placeholder="Name here" v-model="name" />
      </h2>
    </section>

    <section class="create-todo">
      <h3>CREATE A TODO</h3>
      <AddTodo @addTodo="addTodo" />
    </section>
    <section class="todo-list">
      <h3>TODO LIST</h3>
      <DisplayTodo :todos="todos" @removeTodo="removeTodo" />
    </section>
  </main>
</template>

<script setup>
import { ref, onMounted, computed, watch } from "vue";
import AddTodo from "./components/AddTodo.vue";
import DisplayTodo from "./components/DisplayTodo.vue";

// ref: Creates a reactive reference to a value.
// onMounted: Runs code after a component is added to the webpage.
// computed: Calculates a value based on other values.
// watch: Performs an action when a specific value changes.

const todos = ref([]);
const name = ref("");

const todos_asc = computed(() =>
  todos.value.sort((a, b) => {
    return b.createdAt - a.createdAt;
  })
);

// This function adds a todo to the todos array.
const addTodo = (todo) => {
  // Add a new todo to the todos array
  todos.value.push({
    content: todo.content,
    category: todo.category,
    done: false,
    createdAt: new Date().getTime(),
  });
};

// This function removes a todo from the todos array.
const removeTodo = (todo_params) => {
  todos.value = todos.value.filter((todo) => todo !== todo_params);
};

// This watch performs an action when the todos value changes.
watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true }
);

// This watch performs an action when the name value changes.
watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});
</script>
