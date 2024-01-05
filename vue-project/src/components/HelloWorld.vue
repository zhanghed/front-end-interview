<script setup lang="ts">
defineProps<{
  msg: string[];
}>();
</script>

<template>
  <div>
    <h1>{{ msg }}</h1>
  </div>
  <div class="a">
    <div class="b"></div>
  </div>
</template>

<style scoped>
.a {
  width: 200px;
  height: 200px;
  background-color: aquamarine;

  display: flex;
  justify-content: center;
  align-items: center;
}
.b {
  width: 100px;
  height: 100px;
  background-color: antiquewhite;
}
</style>
