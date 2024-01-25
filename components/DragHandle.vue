<script setup lang="ts">
import { DRAG_HANDLE_CLASS } from "../utils/constants.ts";
import { DragHandleSizes } from "../types";

const dragHandleClass = computed(() => DRAG_HANDLE_CLASS.replace(".", ""));
const props = defineProps<{
  size: DragHandleSizes;
}>();

const sizeClass = computed(() =>
  props.size == DragHandleSizes.SMALL ? "size-3 mt-1" : "size-4"
);
</script>

<template>
  <span class="cursor-move items-start flex" :class="dragHandleClass">
    <svg
      class="text-slate-900"
      :class="sizeClass"
      aria-hidden="true"
      xmlns="http://www.w3.org/2000/svg"
      fill="none"
      viewBox="0 0 24 24"
    >
      <path
        stroke="currentColor"
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M4 16h13M4 16l4-4m-4 4 4 4M20 8H7m13 0-4 4m4-4-4-4"
      />
    </svg>
  </span>
</template>
