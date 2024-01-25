<script setup lang="ts">
import { ref } from "vue";
import draggable from "vuedraggable";
import { nanoid } from "nanoid";
import { Task, type Column } from "../types/index.ts";
import TrelloBoardTask from "./TrelloBoardTask.vue";
import DragHandle from "./DragHandle.vue";
import { DRAG_HANDLE_CLASS } from "../utils/constants.ts";

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
      {
        id: nanoid(),
        title: "Prepare a workshop for Frontend Guild",
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
  <div>
    <draggable
      v-model="columns"
      group="columns"
      :animation="250"
      :handle="DRAG_HANDLE_CLASS"
      item-key="id"
      class="board__columns | flex gap-6 overflow-x-auto items-start py-10"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="bg-purple-100 rounded-xl px-2 py-3 min-w-[250px]">
          <header
            class="flex justify-between items-center text-xl font-semibold px-2 mb-3"
          >
            <div class="flex gap-2 items-center">
              <DragHandle />
              {{ column.title }}
            </div>
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
          <draggable
            v-model="column.tasks"
            group="tasks"
            :handle="DRAG_HANDLE_CLASS"
            :animation="250"
            item-key="id"
          >
            <template #item="{ element: task }: { element: Task }">
              <TrelloBoardTask :task="task" />
            </template>
          </draggable>
          <footer>
            <button
              class="hover:bg-purple-50 hover:text-slate-900 rounded-lg text-slate-500 transition-colors hover:shadow-sm px-2 py-1 w-full text-left"
            >
              + Add a card
            </button>
          </footer>
        </div>
      </template>
    </draggable>
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
