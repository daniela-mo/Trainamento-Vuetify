<template>
  <div>
    <v-expansion-panels flat>
      <v-expansion-panel>
        <v-expansion-panel-header>
          Cadastro de séries
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          <template>
            <v-simple-table dark>
              <template v-slot:default>
                <thead>
                  <tr>
                    <th class="text-left">
                      Nome
                    </th>
                    <th class="text-left">
                      Estágio
                    </th>
                    <th class="text-left">
                      Genero
                    </th>
                    <th class="text-left">
                      Plataforma
                    </th>
                    <th class="text-left">
                      Temporadas
                    </th>
                    <th class="text-left">
                      Ano
                    </th>
                    <th class="text-left">
                      Classificação
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="item in desserts" :key="item.id">
                    <td>{{ item.name }}</td>
                    <td>{{ item.phase }}</td>
                    <td>{{ item.gender }}</td>
                    <td>{{ item.plataform }}</td>
                    <td>{{ item.seasons }}</td>
                    <td>{{ item.year }}</td>
                    <td>{{ item.age }}</td>
                    <td>
                      <a
                        href="#"
                        @click="(dialogEdit = true), carregarInfo($event, item)"
                        ><img src="@/assets/editar.svg" alt="Editar"
                      /></a>
                      <a href="#" @click="deletarSerie($event, item.id)"
                        ><img src="@/assets/excluir.svg" alt="Excluir"
                      /></a>
                    </td>
                  </tr>
                </tbody>
              </template>
            </v-simple-table>
          </template>
          <div class="d-flex justify-end">
            <v-btn
              class="mt-5 d-flex"
              fab
              dark
              large
              color="#30dbc7"
              @click="dialog = true"
              ><v-icon dark>mdi-plus</v-icon></v-btn
            >
          </div>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <RegisterSeries
      :dialog="dialog"
      :close="close"
      :carregarSeries="carregarSeries"
    />
    <EditSeries
      :dialogEdit="dialogEdit"
      :close="close"
      :carregarSeries="carregarSeries"
    />
  </div>
</template>

<script>
import RegisterSeries from "@/components/RegisterSeries";
import EditSeries from "@/components/EditSeries";
import axios from "axios";

export default {
  components: {
    RegisterSeries,
    EditSeries,
  },

  data() {
    return {
      dialog: false,
      dialogEdit: false,
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
      desserts: [],
    };
  },
  mounted() {
    this.carregarSeries();
  },
  methods: {
    async carregarSeries() {
      const { data } = await axios.get("http://localhost:3000/desserts");
      this.desserts = data;
    },
    close() {
      this.dialog = false;
      this.dialogEdit = false;
    },
    async deletarSerie(e, id) {
      e.preventDefault();

      const { data } = await axios.delete(
        `http://localhost:3000/desserts/${id}`
      );

      this.carregarSeries();
    },
    carregarInfo(e, item) {
      e.preventDefault();
      this.editar.id = item.id;
      this.editar.name = item.name;
      this.editar.phase = item.phase;
      this.editar.gender = item.gender;
      this.editar.plataform = item.plataform;
      this.editar.seasons = item.seasons;
      this.editar.year = item.year;
      this.editar.age = item.age;
    },
  },
};
</script>
