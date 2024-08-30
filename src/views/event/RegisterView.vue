<script setup lang="ts">
import { toRef } from 'vue'
import type { Event } from '@/types'
import { useRouter } from 'vue-router'
import { useMessageStore } from '@/stores/message'

const props = defineProps<{
  event: Event
  id: String
}>()
// eslint-disable-next-line @typescript-eslint/no-unused-vars
// const { event } = toRef(props)
const event = toRef(props, 'event')
const router = useRouter()
const store = useMessageStore()

const register = () => {
  store.updateMessage('You are successfully registered for ' + props.event.title)
  setTimeout(() => {
    store.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view', params: { id: props.event.id } })
}
</script>

<template>
  <p class="text-gray-700 mb-4">Register for the event here</p>
  <button
    @click="register"
    class="px-5 py-2.5 bg-green-500 text-white font-bold rounded-md hover:bg-green-400 active:bg-green-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md"
  >
    Register
  </button>
</template>
