<template>
  <v-form>
    <v-container fluid>
      <v-col sm="12" md="8" lg="8" centered>
        <v-text-field
          name="diaEvent"
          label="Dia do evento"
          required
          v-model="diaEvent"
        ></v-text-field>

        <v-row justify="space-around" align="center">
          <v-col style="width: 350px; flex: 0 1 auto">
            <h2 class="text-center">HORÁRIO DE INICIO</h2>
            <v-time-picker
              name="horaInicio"
              label="Hora de inicio"
              format="24hr"
              required
              v-model="horaInicio"
              color="green lighten-1"
            ></v-time-picker>
          </v-col>

          <v-col style="width: 350px; flex: 0 1 auto">
            <h2 class="text-center">HORÁRIO DE TERMINO</h2>
            <v-time-picker
              name="horaTermino"
              label="Hora de termino"
              format="24hr"
              required
              v-model="horaTermino"
              header-color="primary"
            ></v-time-picker>
          </v-col>
        </v-row>

        <v-text-field
          name="qtdePessoas"
          label="Quantidade de pessoas"
          required
          v-model="qtdePessoas"
          type="number"
        ></v-text-field>
        <v-text-field
          name="tempDesejada"
          label="Temperatura desejada"
          required
          v-model="tempDesejada"
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
      diaEvent: '',
      horaInicio: '',
      horaTermino: '',
      qtdePessoas: '',
      tempDesejada: '',
      selectedRoom: '',
      itemsList: [],
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
          diaEvent: this.diaEvent,
          horaInicio: this.horaInicio,
          horaTermino: this.horaTermino,
          qtdePessoas: this.qtdePessoas,
          tempDesejada: Number(this.tempDesejada),
          Room: {
            connect: {
              id: Number(this.selectedRoom),
            },
          },
        }
        await this.$axios.post('/events', body)
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
