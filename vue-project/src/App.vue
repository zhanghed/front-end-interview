<script setup lang="ts">
import { onMounted, ref } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
let msg = ref(["a", "b"]);
onMounted(() => {
  setTimeout(() => {
    msg.value.push("c");
  }, 2000);
});
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />
    <div class="wrapper">
      <HelloWorld :msg="msg" />
    </div>
  </header>
</template>

<style scoped></style>
