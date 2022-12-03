<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-form>
    <v-container fluid>
      <v-row justify="center">
        <v-col sm="12" md="8" lg="8" centered>
          <v-text-field
            v-model="description"
            name="description"
            label="Descrição do evento"
            required
          ></v-text-field>

          <v-text-field
            v-model="diaEvent"
            name="diaEvent"
            type="date"
            label="Dia do evento"
            required
          ></v-text-field>

          <v-row justify="space-around" align="center">
            <v-col style="width: 350px; flex: 0 1 auto">
              <h2 class="text-center">HORÁRIO DE INICIO</h2>
              <v-time-picker
                v-model="horaInicio"
                name="horaInicio"
                label="Hora de inicio"
                format="24hr"
                required
                :max="horaTermino"
                color="green lighten-1"
              ></v-time-picker>
            </v-col>

            <v-col style="width: 350px; flex: 0 1 auto">
              <h2 class="text-center">HORÁRIO DE TERMINO</h2>
              <v-time-picker
                v-model="horaTermino"
                name="horaTermino"
                label="Hora de termino"
                format="24hr"
                required
                :min="horaInicio"
                header-color="primary"
              ></v-time-picker>
            </v-col>
          </v-row>

          <v-text-field
            v-model="qtdePessoas"
            name="qtdePessoas"
            label="Quantidade de pessoas"
            required
            type="number"
          ></v-text-field>
          <v-text-field
            v-model="tempDesejada"
            name="tempDesejada"
            label="Temperatura desejada"
            required
          ></v-text-field>
          <v-autocomplete
            v-model="selectedRoom"
            :items="items"
            placeholder="Escolha a sala"
          ></v-autocomplete>
          <v-btn color="primary" @click="create">Adicionar evento</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
import { parseISO } from 'date-fns'

export default {
  data() {
    return {
      diaEvent: '',
      horaInicio: '',
      horaTermino: '',
      qtdePessoas: '',
      tempDesejada: '',
      selectedRoom: '',
      description: '',
      itemsList: [],
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
          startDate: parseISO(`${this.diaEvent}T${this.horaInicio}`),
          endDate: parseISO(`${this.diaEvent}T${this.horaTermino}.000Z`),
          description: this.description,
          amountPeople: parseInt(this.qtdePessoas),
          desiredTemperature: Number(this.tempDesejada),
          roomId: Number(this.selectedRoom),
        }
        await this.$axios.post('/events', body)
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>
