<template>
  <main class="mainWrapper">
    <BackButton />
    <div class="flex flex-row h-screen bg-gray-100 rounded-md">
      <div class="w-1/4 border-r border-gray-300 bg-gray-800">
        <div class="px-4 py-2 font-bold text-lg text-gray-50">Notes</div>
        <div class="overflow-y-auto">
          <div
            v-for="(note, index) in notes"
            :key="note.id"
            class="flex items-center px-4 py-2 hover:bg-gray-100 hover:text-gray-800 cursor-pointer text-gray-100"
            :class="{ 'bg-gray-100': index === selectedNoteIndex }"
            @click="selectNote(index)"
          >
            <div class="w-4 h-4 mr-2 rounded-full bg-gray-800"></div>
            <div
              class="flex-1 truncate"
              :class="{ 'text-gray-800': index === selectedNoteIndex }"
            >
              {{ note.title }}
            </div>
          </div>
        </div>
      </div>
      <div class="flex-1 px-4 py-2">
        <div v-if="selectedNote" class="flex flex-col h-full">
          <div class="flex items-center mb-4">
            <div class="w-4 h-4 mr-2 rounded-full bg-gray-800"></div>
            <div class="font-bold text-lg">{{ selectedNote.title }}</div>
          </div>
          <div
            class="flex-1 overflow-y-auto"
            v-html="selectedNote.content"
          ></div>

          <QuillEditor theme="snow" />
        </div>

        <div v-else class="flex items-center justify-center h-full">
          <div class="text-gray-500">Select a note to view</div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import BackButton from "../components/BackButton.vue";
import { QuillEditor } from "@vueup/vue-quill";
import "@vueup/vue-quill/dist/vue-quill.snow.css";

const notes = [
  {
    id: 1,
    title: "Note 1",
    content: "<p>This is the content of note 1</p>",
  },
  {
    id: 2,
    title: "Note 2",
    content: "<p>This is the content of note 2</p>",
  },
  {
    id: 3,
    title: "Note 3",
    content: "<p>This is the content of note 3</p>",
  },
  {
    id: 4,
    title: "Note 4",
    content: "<p>This is the content of note 4</p>",
  },
];

const selectedNoteIndex = null;

function selectNote(index) {
  selectedNoteIndex = index;
}

const selectedNote = () => {
  if (selectedNoteIndex === null) {
    return null;
  }
  return notes[selectedNoteIndex];
};
</script>

<style>
.note-taking-app {
  font-family: "Syne", sans-serif;
}
</style>
