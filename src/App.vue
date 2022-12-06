<template>

  <main class="py-8 relative">

    <!--Header-->
    <header class="container mx-auto lg:px-32 px-4 ">
      <div class="flex justify-between items-center">
        <h1 class="text-2xl font-bold text-white">VUE JS 3 NOTES</h1>
        <button class="" @click="show = !show">
          <svg class="w-10 h-10 rounded-full text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"
               xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M12 9v3m0 0v3m0-3h3m-3 0H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"></path>
          </svg>
        </button>
      </div>
    </header>
    <!--Header End-->

    <!--Note Card-->
    <section class="container mx-auto px-4 lg:px-32 py-10">
      <div class="grid lg:grid-cols-4 gap-4">
        <article v-for="(note, index) in notes"
                 :key="note.id"
                 class="rounded-lg p-4 space-y-4 hover:scale-105 transition duration-300 w-auto bg-gradient-to-r from-cyan-500 to-blue-500">
          <p class="text-white">{{ note.text }}</p>
          <p class="font-medium text-white">{{ note.date.toLocaleDateString('en-US') }}</p>
          <button @click="deleteNote(index)" class="text-white">Delete</button>
        </article>
      </div>
    </section>
    <!--Note Card End-->

    <!--Popup-->
    <section v-if="show" class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity">
      <div class="absolute relative  min-h-screen m-auto flex justify-center items-center z-10 opacity-100 ">
        <div class="flex min-h-full sm:items-center sm:p-0 bg-white w-1/2 rounded-lg ">
          <div class="p-8 w-full">
            <div class="flex justify-between pb-4 items-center">
              <h1 class="font-bold text-xl">Add New Note</h1>
              <button @click="show = false" class="flex bg-red-500 px-4 py-2 rounded-lg text-white">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"
                     xmlns="http://www.w3.org/2000/svg">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                </svg>
                Cancel
              </button>
            </div>
            <div class="space-y-2">
              <label for="notes" class="block">Notes</label>
              <textarea v-model.trim="newNote" name="" id="" cols="30" rows="10"
                        class="border border-1 border-gray-700 w-full rounded-lg"></textarea>
              <p v-if="errorMsg">{{ errorMsg }}</p>
              <div class="flex justify-end mt-4">
                <button @click="addNote" class="bg-green-500 px-4 py-2 rounded-lg text-white w-full">Add Post</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!--Popup-->

  </main>
</template>

<script setup>
import {ref} from "vue";

let show = ref(false);
const errorMsg = ref('');
const newNote = ref('');
const notes = ref([]);

function getRandomColor() {
  return '#' + (Math.random() * 0xFFFFFF << 0).toString(16);
}

function addNote() {
  if (newNote.value.length < 10) {
    return errorMsg.value = 'Character must be more than 10'
  }
  notes.value.push({
    id: Math.floor(Math.random() * 9999999999),
    text: newNote.value,
    date: new Date(),
    bgColor: getRandomColor(),
  });
  show.value = false;
  newNote.value = '';
  errorMsg.value = '';
}

function deleteNote(index) {
  notes.value.splice(index, 1);
}


</script>
