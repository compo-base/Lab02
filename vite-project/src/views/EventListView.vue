<script setup lang="ts">
import EventCard from '../components/EventCard.vue'
import EventOrganizer from '../components/EventOrganizer.vue'
import { events } from '@/event_type'
import type { EventItem } from './type'
import { ref } from 'vue'
import type { Ref } from 'vue'
import EventService from '@/services/EventService'
const events: Ref<Array<EventItem>> = ref([])
EventService.getEvent().then((response) => {
  events.value = response.data
})
</script>

<template>
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
