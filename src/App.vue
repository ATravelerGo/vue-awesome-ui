<script setup lang="ts">
import TimeLine from './components/TimeLine/index.vue'
import TextArea from './components/TextArea/index.vue';
</script>

<template>
  <div>
    时间轴：
    <TimeLine style="width: 302px;height: 500px" />
  </div>
  <hr>
  <div>
    输入框：
    <TextArea></TextArea>
  </div>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
