<script setup lang="ts">
import { RouterLink, RouterView, useRouter, useRoute } from 'vue-router'
import { useMessageStore } from './stores/message'
import { storeToRefs } from 'pinia'
import { ref } from 'vue'

const perPage = ref(2)
const router = useRouter()
const route = useRoute()
const store = useMessageStore()
const { message } = storeToRefs(store)

function updatePerPage(size: number) {
  perPage.value = size
  router.push({ name: 'event-list-view', query: { page: 1, perPage: size } })
}
</script>

<template>
  <div class="text-center font-sans text-gray-700 antialiased">
    <header>
      <div id="flashMessage" class="animate-yellofade" v-if="message">
        <h4>{{ message }}</h4>
      </div>
      <div class="wrapper">
        <nav class="py-6">
          <RouterLink
            class="font-bold text-gray-700"
            exact-active-class="text-green-500"
            :to="{ name: 'event-list-view' }"
            >Event</RouterLink
          >
          <RouterLink
            class="font-bold text-gray-700"
            exact-active-class="text-green-500"
            :to="{ name: 'about' }"
            >About</RouterLink
          >
          <RouterLink
            class="font-bold text-gray-700"
            exact-active-class="text-green-500"
            :to="{ name: 'student' }"
            >Student</RouterLink
          >
        </nav>
      </div>
    </header>
    <!-- <div class="pagination-controls flex space-x-4 my-5">
      <button class="px-5 py-2.5 bg-blue-500 text-white font-bold rounded-md hover:bg-blue-400 active:bg-blue-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md" @click="updatePerPage(1)">Show 1 per page</button>
      <button class="px-5 py-2.5 bg-blue-500 text-white font-bold rounded-md hover:bg-blue-400 active:bg-blue-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md" @click="updatePerPage(2)">Show 2 per page</button>
      <button class="px-5 py-2.5 bg-blue-500 text-white font-bold rounded-md hover:bg-blue-400 active:bg-blue-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md" @click="updatePerPage(3)">Show 3 per page</button>
      <button class="px-5 py-2.5 bg-blue-500 text-white font-bold rounded-md hover:bg-blue-400 active:bg-blue-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md" @click="updatePerPage(4)">Show 4 per page</button>
      <button class="px-5 py-2.5 bg-blue-500 text-white font-bold rounded-md hover:bg-blue-400 active:bg-blue-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md" @click="updatePerPage(5)">Show 5 per page</button>
      <button class="px-5 py-2.5 bg-blue-500 text-white font-bold rounded-md hover:bg-blue-400 active:bg-blue-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md" @click="updatePerPage(6)">Show 6 per page</button>
    </div> -->
    <RouterView :key="$route.fullPath" />
  </div>
</template>

<!-- <style>
@keyframes yellofade {
  from {
    background-color: yellow;
  }
  to {
    background-color: transparent;
  }
}

#flashMessage {
  animation: yellofade 3s ease-in-out;
}
</style> -->
