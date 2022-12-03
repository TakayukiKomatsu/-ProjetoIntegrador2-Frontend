<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-container class="fill-height align-start" fluid>
    <v-btn color="success mb-4" nuxt to="/event/new">
      <v-icon> mdi-plus </v-icon>
      Adicionar novo evento</v-btn
    >
    <v-data-table :headers="headers" :items="events" class="content">
      <template #item.startDate="{ item }">
        {{ new Date(formatTime(item.startDate)).toLocaleString('pt-BR', {}) }}
      </template>
      <template #item.endDate="{ item }">
        {{ new Date(formatTime(item.endDate)).toLocaleString('pt-BR', {}) }}
      </template>

      <template #item.ACTime="{ item }">
        {{ new Date(formatTime(item.ACTime)).toLocaleString('pt-BR', {}) }}
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
import { addHours } from 'date-fns'
export default {
  data() {
    return {
      events: [],
      headers: [
        {
          text: 'Inicio',
          align: 'center',
          value: 'startDate',
        },
        {
          text: 'Término',
          align: 'center',
          value: 'endDate',
        },
        {
          text: 'Descrição',
          align: 'center',
          value: 'description',
        },
        {
          text: 'Temperatura Desejada',
          align: 'center',
          value: 'desiredTemperature',
        },
        {
          text: 'Quantidade de pessoas',
          align: 'center',
          value: 'amountPeople',
        },
        {
          text: 'Horário do acionamento do ar condicionado',
          align: 'center',
          value: 'ACTime',
        },
      ],
    }
  },
  created() {
    this.fetch()
  },
  methods: {
    async fetch() {
      const { data } = await this.$axios.get('/events')
      this.events = data
    },
    formatTime(time) {
      return addHours(new Date(time), 3)
    },
  },
}
</script>
