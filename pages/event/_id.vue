<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
import EventService from '~/services/EventService'

export default {
  async asyncData({ error, params }) {
    try {
      const { data } = await EventService.getEvent(params.id)

      return {
        event: data,
      }
    } catch (err) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events #' + params.id,
      })
    }
  },
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about ' + this.event.title,
        },
      ],
    }
  },
}
</script>
