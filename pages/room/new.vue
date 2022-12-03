<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-form>
    <v-container fluid>
      <v-row justify="center" class="fill-height">
        <v-col sm="12" md="8" lg="8" centered>
          <v-text-field
            v-model="descricao"
            name="descricao"
            label="Descriçao da sala"
            required
          ></v-text-field>
          <v-text-field
            v-model="estado"
            name="estado"
            label="Estado"
            required
          ></v-text-field>
          <v-text-field
            v-model="cidade"
            name="cidade"
            label="Cidade"
            required
          ></v-text-field>
          <v-text-field
            v-model="pais"
            name="pais"
            label="País"
            required
          ></v-text-field>
          <v-text-field
            v-model="salaLocal"
            name="salaLocal"
            label="Local da sala"
            required
          ></v-text-field>

          <v-btn color="primary" @click="create">Adicionar sala</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  data() {
    return {
      descricao: '',
      cidade: '',
      estado: '',
      pais: '',
      salaLocal: '',
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
        aux.text = e.descricao
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
          description: this.descricao,
          city: this.cidade,
          state: this.estado,
          country: this.pais,
          address: this.salaLocal,
        }
        await this.$axios.post('/rooms', body)
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>
