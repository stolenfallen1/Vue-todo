<template>
  <div class="list">
    <div v-for="todo in todos" :class="`todo-item ${todo.done && 'done'}`">
      <label>
        <input type="checkbox" v-model="todo.done" />
        <span :class="`bubble ${todo.category}`"></span>
      </label>
      <div class="todo-content">
        <input type="text" v-model="todo.content" />
      </div>
      <div class="actions">
        <button class="delete" @click="removeTodo(todo)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  todos: {
    type: Array,
    required: true,
  },
});

const emits = defineEmits(["removeTodo"]);
const removeTodo = (id) => {
  emits("removeTodo", id);
};
</script>

<style lang="scss" scoped></style>
