<script setup lang="ts">
import { useEventStore } from '@/stores/event';
import { storeToRefs } from 'pinia';

const store = useEventStore()
const { event } = storeToRefs(store)

</script>

<template>
  <div v-if="event" class="p-6">
    <h1 class="text-2xl font-bold text-gray-800 mb-4">{{ event.title }}</h1>
    <nav class="mb-6">
      <Router-link 
        :to="{ name: 'event-detail-view'}"
        class="text-blue-500 hover:underline"
      >
        Details
      </Router-link>
      <span class="mx-2">|</span>
      <Router-link 
        :to="{ name: 'event-register-view'}"
        class="text-blue-500 hover:underline"
      >
        Register
      </Router-link>
      <span class="mx-2">|</span>
      <Router-link 
        :to="{ name: 'event-edit-view'}"
        class="text-blue-500 hover:underline"
      >
        Edit
      </Router-link>
    </nav>
    <RouterView :event="event" />
  </div>
</template>
