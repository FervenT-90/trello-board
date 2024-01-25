<script setup lang="ts">
import { ref } from "vue";
import { type Column } from "../types/index.ts";
import { nanoid } from "nanoid";
import TrelloBoardTask from "./TrelloBoardTask.vue";

const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: "Backlog",
    tasks: [
      {
        id: nanoid(),
        title: "Learn Drag & Drop in Vue",
        createdAt: new Date(),
      },
    ],
  },
  {
    id: nanoid(),
    title: "In Progress",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Blocked",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Documentation",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Done",
    tasks: [],
  },
]);
</script>
<template>
  <div class="board__columns | flex gap-6 overflow-x-auto items-start py-10">
    <div
      v-for="column in columns"
      :key="column.id"
      class="bg-purple-100 rounded-xl px-2 py-3 min-w-[250px]"
    >
      <header
        class="flex justify-between items-center text-xl font-semibold px-2 mb-3"
      >
        {{ column.title }}
        <button
          class="flex justify-center items-center hover:bg-purple-50 size-8 rounded-lg transition-colors -mr-2 hover:shadow-sm"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M6.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM12.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM18.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0Z"
            />
          </svg>
        </button>
      </header>
      <TrelloBoardTask
        v-for="task in column.tasks"
        :key="task.id"
        :task="task"
      />
      <footer>
        <button
          class="hover:bg-purple-50 hover:text-slate-900 rounded-lg text-slate-500 transition-colors hover:shadow-sm px-2 py-1 w-full text-left"
        >
          + Add a card
        </button>
      </footer>
    </div>
  </div>
</template>
<style scoped>
.board__columns {
  --sb-track-color: #98989815;
  --sb-thumb-color: #7069b45d;
  --sb-size: 10px;

  scrollbar-color: var(--sb-thumb-color) var(--sb-track-color);
}

.board__columns::-webkit-scrollbar {
  width: var(--sb-size);
}

.board__columns::-webkit-scrollbar-track {
  background: var(--sb-track-color);
  border-radius: 10px;
}

.board__columns::-webkit-scrollbar-thumb {
  background: var(--sb-thumb-color);
  border-radius: 10px;
}
</style>
