<script setup lang="ts">
import { type Task } from "../types/index.ts";

defineProps<{
  task: Task;
}>();
</script>

<template>
  <div
    :title="task.createdAt.toLocaleDateString()"
    class="bg-white p-2 rounded-lg text-slate-800 shadow mb-2"
  >
    <span>{{ task.title }}</span>
  </div>
</template>
