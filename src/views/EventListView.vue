<script setup lang="ts">
import EventService from '@/services/EventService'
import EventCard from '@/components/EventCard.vue'
import { ref, onMounted } from 'vue'

interface Event {
  id: number
  category: string
  title: string
  description: string
  location: string
  date: string
  time: string
  petsAllowed: boolean
  organizer: string
}

const events = ref<[Event]>()
onMounted(() => {
  EventService.getEvents()
    .then((response): void => {
      events.value = response.data
    })
    .catch((e) => console.error(e))
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
