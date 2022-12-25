<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import EventCard from '~/components/EventCard.vue'
import EventService from '~/services/EventService'

export default {
  components: {
    EventCard,
  },
  async asyncData({ error }) {
    try {
      const { data } = await EventService.getEvents()

      return {
        events: data,
      }
    } catch (err) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time, please try again',
      })
    }
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
}
</script>
