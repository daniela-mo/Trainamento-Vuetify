<template>
  <v-row justify="center">
    <v-dialog v-model="dialogEdit" persistent max-width="800px">
      <v-card>
        <v-card-title>
          <span class="text-h5">Alterar séries</span>
        </v-card-title>

        <v-card-text>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Nome"
                hide-details
                outlined
                dense
                v-model="editar.name"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Estágio"
                hide-details
                outlined
                dense
                v-model="editar.phase"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Gênero"
                hide-details
                outlined
                dense
                v-model="editar.gender"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Plataforma"
                hide-details
                outlined
                dense
                v-model="editar.plataform"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Temporadas"
                hide-details
                outlined
                dense
                v-model="editar.seasons"
              />
            </v-col>

            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Ano Lançamento"
                hide-details
                outlined
                dense
                v-model="editar.year"
              />
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                label="Classificação"
                hide-details
                outlined
                dense
                v-model="editar.age"
              />
            </v-col>
          </v-row>
        </v-card-text>

        <v-card-actions>
          <v-spacer />
          <v-btn color="black" outlined @click="close()">
            Fechar
          </v-btn>
          <v-btn color="pink" outlined @click="editarSeries">
            Editar
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
    editar: {
      id: "",
      name: "",
      phase: "",
      gender: "",
      plataform: "",
      seasons: "",
      year: "",
      age: "",
    },
  }),
  props: {
    dialogEdit: Boolean,
    close: Function,
    carregarSeries: Function,
  },
  methods: {
    // async carregarSeries() {
    //   const { data } = await axios.get("http://localhost:3000/desserts");
    //   this.desserts = data;
    // },

    async editarSerie(e) {
      e.preventDefault();
      const { data } = await axios.put(
        `http://localhost:3000/desserts/${this.editar.id}`,
        {
          name: this.editar.name,
          phase: this.editar.phase,
          gender: this.editar.gender,
          plataform: this.editar.plataform,
          seasons: this.editar.seasons,
          year: this.editar.year,
          age: this.editar.age,
        }
      );
      this.dialogEdit = false;
      this.carregarSeries();
    },
  },
};
</script>
