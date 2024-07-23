<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import Event from '@/types/Event'
import EventDetails from '@/components/EventDetails.vue'
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'

const events = ref<Event[]>(null)

onMounted(() =>{
  EventService.getEvents()
    .then((response) =>{
       //console.log(response.data)
      events.value = response.data
    })
    .catch((error) =>{
      console.error('There was an error!', error)
    })
  })
</script>

<template>
  <h1>Events For Good</h1>
  <!--New Element-->
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <EventDetails v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
