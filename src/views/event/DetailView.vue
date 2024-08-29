<script setup lang="ts">
import { toRefs, defineProps, onMounted } from 'vue'
import { type Event } from '@/types'
import { useMessageStore } from '@/stores/message'
import { storeToRefs } from 'pinia'

const props = defineProps<{
  event: Event
  id: String
}>()
const { event } = toRefs(props)
const store = useMessageStore()
const { message } = storeToRefs(store)

onMounted(() => {
  if (message.value) {
    setTimeout(() => {
      store.resetMessage()
    }, 5000)
  }
})
</script>

<template>
  <div v-if="message" id="flashMessage" class="bg-yellow-200 p-4 rounded-md mb-4 animate-yellofade">
    <h4 class="font-semibold">{{ message }}</h4>
  </div>
  <p class="text-gray-700">{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
  <p class="text-gray-600 mt-2">{{ event.description }}</p>
</template>

<style scoped>
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
</style>
