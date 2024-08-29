<script setup lang="ts">
import { toRef } from 'vue'
import { type Event } from '@/types'
import { useRouter } from 'vue-router'
import { useMessageStore } from '@/stores/message'

const props = defineProps<{
    event: Event
    id: String
}>()
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const { event } = toRef(props)
const router = useRouter()
const store = useMessageStore()

const updateEvent = () => {
    store.updateMessage('Event data has been updated')
    setTimeout(() => {
        store.resetMessage()
    }, 5000)
    router.push({ name: 'event-detail-view', params: { id: props.event.id } })
}
</script>

<template>
    <p class="text-gray-700 mb-4">Edit event here</p>
    <button
        @click="updateEvent"
        class="px-5 py-2.5 bg-blue-500 text-white font-bold rounded-md hover:bg-blue-400 active:bg-blue-600 transition-transform transform hover:-translate-y-1 active:translate-y-0 shadow-md"
    >
        Save Changes
    </button>
</template>
