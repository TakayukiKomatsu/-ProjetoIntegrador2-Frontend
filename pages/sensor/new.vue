<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-form class="fill-height">
    <v-container fluid class="fill-height">
      <v-row justify="center" class="fill-height">
        <v-col sm="12" md="8" lg="8" centered>
          <v-autocomplete
            v-model="selectedType"
            name="tipo"
            :items="types"
            label="Tipo do sensor"
            required
          ></v-autocomplete>
          <v-autocomplete
            v-model="selectedRoom"
            :items="items"
            placeholder="Escolha a sala"
          ></v-autocomplete>
          <v-btn color="primary" @click="create">Adicionar sensor</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  data() {
    return {
      selectedRoom: '',
      itemsList: [],
      selectedType: '',
      temperature: '',
      leitura: '',
      interLeitura: '',
      types: [
        {
          text: 'Manual',
          value: 'Manual',
        },
        {
          text: 'Automático',
          value: 'Automático',
        },
      ],
    }
  },
  computed: {
    items() {
      const item = []
      this.itemsList.forEach((e) => {
        const aux = {
          text: null,
          value: null,
        }
        aux.value = e.id
        aux.text = e.description
        item.push(aux)
      })
      return item
    },
  },
  async created() {
    try {
      const response = await this.$axios.get('/rooms/description')
      this.itemsList = response.data
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    async create() {
      try {
        const body = {
          type: this.selectedType,
          roomId: Number(this.selectedRoom),
        }
        await this.$axios.post('/sensors', body)
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>

<style></style>
