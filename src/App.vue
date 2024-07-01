<script setup>
import { ref, watch } from 'vue';
// import list from '@/components/list';
// import Computed from './components/computeds.vue';
// import baseVue from './components/base.vue';
// import HelloWorld from './components/HelloWorld.vue';
// import formModel from './components/formModel.vue';
// import life from './components/life.vue';
import { storeToRefs } from 'pinia';
import { useUserStore } from '@/store/user';
import { useMouse } from "@/utils/hooks";

const userStore = useUserStore();
// 此时userStore 并不是响应式数据 需要变成响应式的
const { name } = storeToRefs(userStore);
// 方法不需要是响应式的 storeToRefs 不会去处理方法 需要去userStore结构
const { updateName } = userStore;

const type = ref('base');
const message = ref('你好👋');

const {x, y} = useMouse();
watch(type, (newType) => {
  console.log(`type is ${newType}`)
}, {immediate: true})
const userPath = ref('/user/456');

function warn(message, event) {
  console.log('event', event);
  // 这里可以访问原生事件
  if (event) {
    event.preventDefault();
  }
  alert(message);
}
</script>

<template>
    <div class="nav-wrapper">
      <div
        class="mr-10"
        :class="{active: type === item}"
        v-for="(item, index) in ['base', 'computed', 'list', 'hello', 'form', 'life', 'user', 'fa']"
        :key="`nav_${index}`"
        @click="type = item"
      >
        <RouterLink :to="`/${item}`">{{item}}</RouterLink>
      </div>
    </div>
  <!-- </div> -->

  <main>
    <router-view />
  </main>
</template>

<style scoped>
.active {
  color: #ff99cc;
}

.border-black {
  border: #9e9eed solid px;
}

.pd-20 {
  padding: 20px;
}

.mr-10 {
  display: inline-block;
  margin-right: 10px;
  color: #ffb0b0;
}
.nav-wrapper {
  color:#ffb0b0;
  height: 64px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: 1px solid rgba(232, 196, 76, 0.4);
}
</style>
