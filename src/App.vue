<script setup lang="ts">
import TimeLine from './components/TimeLine/index.vue'

</script>

<template>
  <div>
    <TimeLine style="width: 302px;height: 500px" />

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
