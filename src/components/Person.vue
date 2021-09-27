<script setup lang="ts">
const props = defineProps<{
  person: string;
  index: number;
}>();

const emit = defineEmits(["remove"]);
const remove = () => {
  emit("remove", props.index);
};
</script>

<template>
  <div class="person">
    <svg
      width="14"
      height="14"
      viewBox="0 0 14 14"
      fill="none"
      class="person-icon"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        fill-rule="evenodd"
        clip-rule="evenodd"
        d="M9.27652 7.28943C10.318 6.56731 11 5.3633 11 4C11 1.79086 9.20914 0 7 0C4.79086 0 3 1.79086 3 4C3 5.44916 3.77063 6.71832 4.92444 7.42005C1.75117 8.6185 0.33208 12.0905 0 14H14C13.8274 12.0154 12.6274 8.34299 9.27652 7.28943Z"
        fill="var(--text-color)"
      />
    </svg>

    {{ props.person }}
    <button class="remove-button" @click="remove">
      <span> + </span>
    </button>
  </div>
</template>
<style scoped>
.person {
  border-bottom: 1px solid var(--darker-color);
  padding: 16px;
  display: flex;
  align-items: center;
}
.remove-button {
  background: transparent;
  outline: none;
  border: none;
  margin-left: auto;
  cursor: pointer;
}
.remove-button span {
  display: inline-block;
  font-size: 20px;
  color: var(--text-color);
  transform: rotate(45deg);
}
.person-icon {
  margin-right: 16px;
}
</style>
