<template>
  <h1>{{ $route.meta.title }}</h1>
  <div>编号：{{ $route.params.id }}</div>
  <div>姓名：小花</div>
  <div>性别：女</div>
  <div>年龄:18</div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const userId = ref(route.params.id);

watchEffect(() => {
  // 请求用户数据
  // fetch(`/user/${userId.value}`).then;
});
</script>
