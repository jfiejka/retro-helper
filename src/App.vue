<script setup lang="ts">
import Randomizer from "./components/Randomizer.vue";
</script>

<template>
  <Randomizer />
</template>

<style>
#app {
  --text-color: #e8e8e8;
  --darker-color: #040f2d;
  --dark-color: #0e1734;
  --primary-color: #0030c0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  height: 100%;
  color: var(--text-color);
}
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;

  background-color: var(--darker-color);
}
</style>
