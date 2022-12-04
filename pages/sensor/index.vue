<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-container class="fill-height align-start" fluid>
    <v-btn color="success mb-4" nuxt to="/sensor/new">
      <v-icon> mdi-plus </v-icon>
      Adicionar novo Sensor</v-btn
    >
    <v-data-table :headers="headers" :items="events" class="content">
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
          text: 'ID da sala',
          align: 'center',
          value: 'roomId',
        },
{
          text: 'ID do sensor',
          align: 'center',
          value: 'id',
        },
        {
          text: 'Tipo',
          align: 'center',
          value: 'type',
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
