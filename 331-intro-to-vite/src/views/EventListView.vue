<script setup lang="ts">
import { ref, onMounted, watchEffect, defineProps, computed } from 'vue'
import EventCard from '@/components/EventCard.vue'
import EventDetails from '@/components/EventDetails.vue'
import EventService from '@/services/EventService'
import { type Event } from '@/types'

const props = defineProps({
  page: {
    type: Number,
    required: true
  },
  perPage: {
    type: Number,
    required: true
  }
})

const events = ref<Event[] | null>(null)
const totalEvents = ref(0)
const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / props.perPage)
  return props.page < totalPages
})

onMounted(() => {
  watchEffect(() => {
    events.value = null
    EventService.getEvents(props.perPage, props.page)
      .then((response) => {
        events.value = response.data
        totalEvents.value = parseInt(response.headers['x-total-count'], 10)
      })
      .catch((error) => {
        console.error('There was an error!', error)
      })
  })
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <EventDetails v-for="event in events" :key="event.id" :event="event" />
    <div class="pagination">
      <RouterLink
        v-if="props.page > 1"
        :to="{ name: 'event-list-view', query: { page: props.page - 1, perPage: props.perPage }}"
        rel="prev"
      >
        &#60; Prev page
      </RouterLink>
      <RouterLink
        v-if="hasNextPage"
        :to="{ name: 'event-list-view', query: { page: props.page + 1, perPage: props.perPage }}"
        rel="next"
      >
        Next Page &#62;
      </RouterLink>
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  width: 290px;
}
.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}
</style>
