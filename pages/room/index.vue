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
      <template #item.actions="{ item }">
        <v-btn nuxt icon>
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
          text: 'Descrição',
          align: 'center',
          value: 'descricao',
        },
        {
          text: 'País',
          align: 'center',
          value: 'pais',
        },
        {
          text: 'Estado',
          align: 'center',
          value: 'estado',
        },
        {
          text: 'Cidade',
          align: 'center',
          value: 'cidade',
        },
        {
          text: 'Local da sala',
          align: 'center',
          value: 'salaLocal',
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
