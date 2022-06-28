<template>
  <v-form>
    <v-container fluid>
      <v-col sm="12" md="8" lg="8" centered>
        <v-text-field
          name="descricao"
          label="Descriçao da sala"
          required
          v-model="descricao"
        ></v-text-field>
        <v-text-field
          name="estado"
          label="Estado"
          required
          v-model="estado"
        ></v-text-field>
        <v-text-field
          name="cidade"
          label="Cidade"
          required
          v-model="cidade"
        ></v-text-field>
         <v-text-field
          name="pais"
          label="País"
          required
          v-model="pais"
        ></v-text-field>
        <v-text-field
          name="salaLocal"
          label="Local da sala"
          required
          v-model="salaLocal"
        ></v-text-field>
      </v-col>

      <v-btn color="primary" @click="create">Criar Sala</v-btn>
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
        "descricao": this.descricao,
        "cidade": this.cidade,
        "estado": this.estado,
        "pais": this.pais,
        "salaLocal": this.salaLocal,
      }
      await this.$axios.post('/rooms', body)
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
