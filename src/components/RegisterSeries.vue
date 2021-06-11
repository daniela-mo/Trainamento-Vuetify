<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="800px">
      <v-card>
        <v-card-title>
          <span class="text-h5">Cadastro de séries</span>
        </v-card-title>

        <v-card-text>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Nome"
                hide-details
                outlined
                dense
                v-model="name"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Estágio"
                hide-details
                outlined
                dense
                v-model="phase"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Gênero"
                hide-details
                outlined
                dense
                v-model="gender"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Plataforma"
                hide-details
                outlined
                dense
                v-model="plataform"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Temporadas"
                hide-details
                outlined
                dense
                v-model="seasons"
              />
            </v-col>

            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Ano Lançamento"
                hide-details
                outlined
                dense
                v-model="year"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Classificação"
                hide-details
                outlined
                dense
                v-model="age"
              />
            </v-col>
          </v-row>
        </v-card-text>

        <v-card-actions>
          <v-spacer />
          <v-btn color="black" outlined @click="close()">
            Fechar
          </v-btn>
          <v-btn color="pink" outlined @click="registerseries">
            Cadastrar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    name: "",
    phase: "",
    gender: "",
    plataform: "",
    seasons: "",
    year: "",
    age: "",
  }),

  props: {
    dialog: Boolean,
    close: Function,
    carregarSeries: Function,
  },
  mounted() {
    this.carregarSeries();
  },

  methods: {
    async registerseries(e) {
      e.preventDefault();
      const { data } = await axios.post("http://localhost:3000/desserts", {
        name: this.name,
        phase: this.phase,
        gender: this.gender,
        plataform: this.plataform,
        seasons: this.seasons,
        year: this.year,
        age: this.age,
      });
      this.dialog = false;

      this.carregarSeries();
      (this.name = ""),
        (this.phase = ""),
        (this.gender = ""),
        (this.plataform = ""),
        (this.seasons = ""),
        (this.year = ""),
        (this.age = "");
    },
    // async carregarSeries() {
    //   const { data } = await axios.get("http://localhost:3000/desserts");
    //   this.desserts = data;
    // },
  },
};
</script>
