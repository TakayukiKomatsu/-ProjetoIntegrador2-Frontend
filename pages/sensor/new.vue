<template>
  <v-form>
    <v-container fluid>
      <v-col sm="12" md="8" lg="8" centered>
        <v-autocomplete
          name="tipo"
          :items="types"
          label="Tipo do sensor"
          required
          v-model="selectedType"
        ></v-autocomplete>
        <v-text-field
          name="temperatura"
          label="Temperatura"
          required
          v-model="temperature"
        ></v-text-field>
        <v-text-field
          name="Leitura"
          label="Data da leitura"
          v-model="leitura"
        ></v-text-field>
        <v-text-field
          name="InterLeitura"
          label="Intervalo de leitura"
          required
          v-model="interLeitura"
        ></v-text-field>
        <v-autocomplete
          :items="items"
          v-model="selectedRoom"
          placeholder="Escolha a sala"
        ></v-autocomplete>
      </v-col>

      <v-btn color="primary" @click="create">Criar evento</v-btn>
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
          tipo: this.selectedType,
          temperatura: Number(this.temperature),
          leitura: this.leitura,
          interLeitura: this.interLeitura,
          Room: {
            connect: {
              id: Number(this.selectedRoom),
            },
          },
        }
        await this.$axios.post('/sensors', body)
      } catch (error) {
        console.log(error)
      }
    },
  },
  computed: {
    items() {
      let item = []
      this.itemsList.forEach((e) => {
        let aux = {
          text: null,
          value: null,
        }
        aux.value = e.id
        aux.text = e.descricao
        item.push(aux)
      })
      return item
    },
  },
}
</script>

<style></style>
