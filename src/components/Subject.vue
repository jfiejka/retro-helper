<script setup lang="ts">
const props = defineProps<{
  subject: string;
  index: number;
}>();
const emit = defineEmits(["remove"]);
const remove = () => {
  emit("remove", props.index);
};
</script>

<template>
  <div class="subject">
    <svg
      width="14"
      height="14"
      viewBox="0 0 14 14"
      fill="none"
      class="subject-icon"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        fill-rule="evenodd"
        clip-rule="evenodd"
        d="M1 0C0.447693 0 0 0.447723 0 1V5.36365C0 5.91592 0.447693 6.36365 1 6.36365H5.36365C5.91589 6.36365 6.36365 5.91592 6.36365 5.36365V1C6.36365 0.447723 5.91589 0 5.36365 0H1ZM8.63635 0C8.08405 0 7.63635 0.447723 7.63635 1V5.36365C7.63635 5.91592 8.08405 6.36365 8.63635 6.36365H13C13.5522 6.36365 14 5.91592 14 5.36365V1C14 0.447723 13.5522 0 13 0H8.63635ZM7.63635 8.63638C7.63635 8.08411 8.08405 7.63638 8.63635 7.63638H13C13.5522 7.63638 14 8.08411 14 8.63638V13C14 13.5523 13.5522 14 13 14H8.63635C8.08405 14 7.63635 13.5523 7.63635 13V8.63638ZM1 7.63638C0.447693 7.63638 0 8.08411 0 8.63638V13C0 13.5523 0.447693 14 1 14H5.36365C5.91589 14 6.36365 13.5523 6.36365 13V8.63638C6.36365 8.08411 5.91589 7.63638 5.36365 7.63638H1Z"
        fill="var(--text-color)"
      />
    </svg>

    {{ props.subject }}
    <button class="remove-button" @click="remove">
      <span> + </span>
    </button>
  </div>
</template>
<style scoped>
.subject {
  border-bottom: 1px solid var(--darker-color);
  padding: 16px;
  display: flex;
  align-items: center;
}
.subject-icon {
  margin-right: 16px;
  fill: var(--darker-color);
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
</style>
