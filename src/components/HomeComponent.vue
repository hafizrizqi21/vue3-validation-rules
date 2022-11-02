<template>
  <div>
    <input @input="(val) => validate(val)" />
    <div v-if="isError" class="error">{{ errorMessage }}</div>
  </div>
</template>

<script setup>
import { ref } from "vue";

let isError = ref(false);
let errorMessage = ref("");
let rules = [
  (val) => !!val || "Harus diisi",
  (val) => val.length >= 8 || "Minimal 8 karakter",
];
const validate = (val) => {
  const text = val.target.value;
  for (const rule of rules) {
    console.log(typeof rule(text) === "string");
    if (typeof rule(text) === "string") {
      errorMessage.value = rule(text);
      isError.value = true;
      return;
    } else {
      errorMessage.value = rule("");
      isError.value = false;
    }
  }
  console.log(errorMessage.value, isError.value);
};
</script>

<style>
.error {
  color: red;
}
</style>
