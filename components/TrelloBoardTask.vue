<script setup lang="ts">
import { DragHandleSizes, type Task } from "../types/index.ts";
import DragHandle from "./DragHandle.vue";

defineProps<{
  task: Task;
}>();
</script>

<template>
  <div
    :title="task.createdAt.toLocaleDateString()"
    class="bg-white p-2 rounded-lg text-slate-800 shadow mb-2 flex"
  >
    <DragHandle class="pr-2" :size="DragHandleSizes.SMALL" />
    <span>{{ task.title }}</span>
  </div>
</template>
