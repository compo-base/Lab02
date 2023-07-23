<script setup lang="ts">
import EventCard from '../components/EventCard.vue'
import EventOrganizer from '../components/EventOrganizer.vue'
import { events } from '@/event_type'
import type { EventItem } from './type'
import { ref } from 'vue'
import EventServices from '@/services/EventService'
import type { Ref } from 'vue'
const event: Ref<Array<EventItem>> = ref([])
EventServices.get().then((response) => {
  event.value = response.data
})
</script>

<template>
  <h1>Event for Good</h1>
  <main class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event"></EventCard>
    <EventOrganizer v-for="event in events" :key="event.id" :event="event"></EventOrganizer>
  </main>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
