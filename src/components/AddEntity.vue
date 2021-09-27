<script setup lang="ts">
import { computed } from "@vue/reactivity";

const props = defineProps<{
  value: string;
}>();
const emit = defineEmits(["update:value", "add"]);
const onEnterClick = (event: KeyboardEvent) => {
  if (event.key === "Enter") {
    emit("add", text.value);
  }
};
const onButtonClick = () => {
  emit("add", text.value);
};
const text = computed({
  get() {
    return props.value;
  },
  set(val) {
    emit("update:value", val);
  },
});
</script>

<template>
  <div class="input-wrapper">
    <input
      placeholder="Add here..."
      type="text"
      class="input"
      v-model="text"
      @keypress="onEnterClick"
    />
    <button class="add-button" @click="onButtonClick">+</button>
  </div>
</template>
<style scoped>
.input {
  background-color: var(--darker-color);
  flex: 1;
  padding: 16px;
  outline: none;
  border: none;
  font-size: 16px;
  color: var(--text-color);
}
.input-wrapper {
  display: flex;
}
.add-button {
  background: var(--darker-color);
  color: var(--text-color);
  font-size: 24px;
  padding: 16px;
  outline: none;
  border: none;
}
</style>
