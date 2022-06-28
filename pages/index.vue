<template>
  <v-calendar
    ref="calendar"
    v-model="value"
    locale="pt-BR"
    :type="type"
    :events="events"
    :event-overlap-mode="mode"
    :event-overlap-threshold="30"
    mode="stack"
  ></v-calendar>
</template>

<script>
export default {
  name: 'IndexPage',
  layout: 'default',

  created() {
    this.getEvents()
  },
  data() {
    return {
      value: '',
      type: 'week',
      mode: 'stack',
      events: [],
      colors: [
        'blue',
        'indigo',
        'deep-purple',
        'cyan',
        'green',
        'orange',
        'grey darken-1',
      ],
    }
  },
  methods: {
    rnd(a, b) {
      return Math.floor((b - a + 1) * Math.random()) + a
    },
    async getEvents() {
      const response = await this.$axios.get(`/events`)
      const eventsInfo = response.data
      let calendarValues = []

      for (let count = 0; count < eventsInfo.length; count++) {
        const event = eventsInfo[count]
        const eventStart = `${event.diaEvent} ${event.horaInicio}`
        const eventFinish = `${event.diaEvent} ${event.horaTermino}`

        calendarValues.push({
          name: null,
          start: eventStart,
          end: eventFinish,
          color: this.colors[this.rnd(0, this.colors.length - 1)],
        })
      }
      this.events = calendarValues
    },
  },
}
</script>
