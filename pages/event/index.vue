<template>
  <v-container class="fill-height align-start" fluid>
    <v-btn color="success mb-4" nuxt to="/event/new">
      <v-icon> mdi-plus </v-icon>
      Adicionar novo evento</v-btn
    >
    <v-data-table :headers="headers" :items="events" class="content">
      <template v-slot:item.actions="{ item }">
        <v-btn @click="" nuxt icon>
          <v-icon> mdi-pencil </v-icon>
        </v-btn>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  created() {
    this.fetch()
  },
  data() {
    return {
      events: [],
      headers: [
        {
          text: 'Dia do evento',
          align: 'center',
          value: 'diaEvent',
        },
        {
          text: 'Inicio',
          align: 'center',
          value: 'horaInicio',
        },
        {
          text: 'Fim',
          align: 'center',
          value: 'horaTermino',
        },
        {
          text: 'Temperatura externa',
          align: 'center',
          value: 'tempExterna',
        },
        {
          text: 'Temperatura Desejada',
          align: 'center',
          value: 'tempDesejada',
        },
        {
          text: 'Horário do acionamento do ar condicionado',
          align: 'center',
          value: 'horaAcionamentoArCondicionado',
        },
        {
          text: '',
          align: 'center',
          sortable: false,
          value: 'actions',
        },
      ],
    }
  },
  methods: {
    async fetch() {
      const { data } = await this.$axios.get('/events')
      this.events = data
    },
  },
}
</script>
