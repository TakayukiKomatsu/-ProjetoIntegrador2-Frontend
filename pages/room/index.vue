<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-container class="fill-height align-start" fluid>
    <v-btn color="success mb-4" nuxt to="/room/new">
      <v-icon> mdi-plus </v-icon>
      Adicionar nova sala</v-btn
    >
    <v-data-table
      :headers="headers"
      :items="events"
      class="content fill-height"
    >
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
          text: 'Descrição',
          align: 'center',
          value: 'description',
        },
        {
          text: 'País',
          align: 'center',
          value: 'country',
        },
        {
          text: 'Estado',
          align: 'center',
          value: 'state',
        },
        {
          text: 'Cidade',
          align: 'center',
          value: 'city',
        },
        {
          text: 'Local da sala',
          align: 'center',
          value: 'address',
        },
      ],
    }
  },
  created() {
    this.fetch()
  },
  methods: {
    async fetch() {
      const { data } = await this.$axios.get('/rooms')
      this.events = data
    },
  },
}
</script>
