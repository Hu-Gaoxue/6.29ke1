<script setup>
import { ref } from 'vue';

defineProps({
  msg: String,
  message: String
});

const count = ref(0);
</script>

<template>
  <h1>{{ msg }}</h1>
  <h2>{{ message }}</h2>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
