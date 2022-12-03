<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-container class="fill-height align-start" fluid>
    <v-btn color="success mb-4" nuxt to="/sensor/new">
      <v-icon> mdi-plus </v-icon>
      Adicionar novo Sensor</v-btn
    >
    <v-data-table :headers="headers" :items="events" class="content">
      <template #item.actions="{ item }">
        <v-btn nuxt icon @click="">
          <v-icon> mdi-pencil </v-icon>
        </v-btn>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      events: [],
      headers: [
        {
          text: 'Tipo',
          align: 'center',
          value: 'tipo',
        },
        {
          text: 'Temperatura',
          align: 'center',
          value: 'temperatura',
        },
        {
          text: 'Leitura',
          align: 'center',
          value: 'leitura',
        },
        {
          text: 'Intervalo de leitura',
          align: 'center',
          value: 'interLeitura',
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
  created() {
    this.fetch()
  },
  methods: {
    async fetch() {
      const { data } = await this.$axios.get('/sensors')
      this.events = data
    },
  },
}
</script>
