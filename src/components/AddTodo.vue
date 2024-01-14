<template>
  <form @submit.prevent="addTodo">
    <h4>What's on your todo list?</h4>
    <input
      type="text"
      placeholder="e.g. make a video"
      v-model="input_content"
    />
    <h4>Pick a category</h4>
    <div class="options">
      <label>
        <input
          type="radio"
          name="category"
          id="category1"
          value="business"
          v-model="input_category"
        />
        <span class="bubble business"></span>
        <div>Business</div>
      </label>
      <label>
        <input
          type="radio"
          name="category"
          id="category1"
          value="personal"
          v-model="input_category"
        />
        <span class="bubble personal"></span>
        <div>Personal</div>
      </label>
    </div>
    <input type="submit" value="Add Todo" />
  </form>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const input_content = ref("");
const input_category = ref(null);
const emit = defineEmits(["addTodo"]);

const addTodo = () => {
  // Check if the input values are empty and return if they are.
  if (input_content.value.trim() === "" || input_category.value === null) {
    // Show alert
    return;
  }
  const todo = {
    content: input_content.value,
    category: input_category.value,
  };
  emit("addTodo", todo);
  input_content.value = "";
  input_category.value = null;
};
</script>

<style lang="scss" scoped></style>
