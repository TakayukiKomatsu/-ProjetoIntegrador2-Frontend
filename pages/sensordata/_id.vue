<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-container class="fill-height align-start" fluid>
    <v-data-table :headers="headers" :items="events" class="content">
      <template #item.time="{ item }">
        {{ new Date(formatTime(item.time)).toLocaleString('pt-BR', {}) }}
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
import { addHours, compareAsc } from 'date-fns'

export default {
  data() {
    return {
      events: [],
      headers: [
        {
          text: 'Temperatura',
          align: 'center',
          value: 'value',
        },
        {
          text: 'Data',
          align: 'center',
          value: 'time',
          sort: (a, b) => compareAsc(a, b),
        },
        {
          text: 'Local',
          align: 'center',
          value: 'topic',
        },
      ],
    }
  },
  created() {
    this.fetch()
  },
  methods: {
    async fetch() {
      const { data } = await this.$axios.get(
        `/sensorData/${this.$route.params.id}`
      )
      this.events = data
    },
    formatTime(time) {
      return addHours(new Date(time), 3)
    },
  },
}
</script>
