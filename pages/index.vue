<template>
  <v-row align="center" class="fill-height">
    <v-col align="center">
      <v-sheet tile height="54" class="d-flex">
        <v-btn icon class="ma-2" @click="$refs.calendar.prev()">
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
        <v-select
          v-model="type"
          :items="types"
          dense
          outlined
          hide-details
          class="ma-2"
          label="type"
        ></v-select>
        <v-btn icon class="ma-2" @click="$refs.calendar.next()">
          <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </v-sheet>
      <v-sheet>
        <v-calendar
          ref="calendar"
          v-model="value"
          :type="type"
          :events="events"
          :event-overlap-mode="mode"
          :event-overlap-threshold="30"
          @change="getEvents"
        ></v-calendar>
      </v-sheet>
    </v-col>
  </v-row>
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
      type: 'month',
      types: ['month', 'week', 'day', '4day'],
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
