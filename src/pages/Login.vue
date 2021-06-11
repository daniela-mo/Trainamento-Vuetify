<template>
  <div class="container" color="#700343">
    <v-card width="400" height="300">
      <v-card-text>
        <!-- <div class="">
      <v-img src="@/assets/logo.svg" />
    </div> -->
        <v-form>
          <v-row>
            <v-col md="12">
              <v-text-field
                filled
                color="#700343"
                label="Usuário"
                clearable
                v-model="email"
                append-icon="face"
                hide-details
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col md="12">
              <v-text-field
                filled
                color="#700343"
                label="Senha"
                clearable
                :append-icon="show ? 'visibility' : 'visibility_off'"
                :type="show ? 'text' : 'password'"
                @click:append="show = !show"
                hide-details
                v-model="senha"
              />
            </v-col>
          </v-row>

          <v-row>
            <v-col class="column" md="3">
              <v-btn
                :loading="loading"
                :disabled="loading"
                color="#700343"
                class="ma-2 white--text"
                @click="submit"
                width="150"
                >Entrar</v-btn
              >
            </v-col>
          </v-row>

          <v-row>
            <v-col md="3">
              <v-btn
                outlined
                width="150"
                color="#700343"
                @click="dialog = true"
              >
                Cadastrar
              </v-btn>
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
      <Register :dialog="dialog" :close="close" />

      <v-snackbar v-model="snackbar">
        {{ snackbarText }}

        <template v-slot:action="{ attrs }">
          <v-btn color="pink" text v-bind="attrs" @click="snackbar = false">
            Close
          </v-btn>
        </template>
      </v-snackbar>
    </v-card>
  </div>
</template>

<script>
import Register from "@/components/Register";
import axios from "axios";
export default {
  data: () => ({
    show: false,
    loader: null,
    loading: false,
    dialog: false,
    email: "",
    senha: "",
    dialog: false,
    snackbar: false,
    snackbarText: "",
    timeout: 2000,
  }),
  watch: {
    loader() {
      const l = this.loader;
      this[l] = !this[l];
      setTimeout(() => (this[l] = false), 3000);
      this.loader = true;
    },
  },
  components: {
    Register,
  },
  methods: {
    close() {
      this.dialog = false;
    },
    async submit() {
      this.loader = "loading";
      const { data } = await axios.get("http://localhost:3000/user", {
        params: {
          email: this.email,
          senha: this.senha,
        },
      });
      if (data.length > 0) {
        this.$router.push("/");
      } else {
        this.snackbarText = "Usuário ou senha incorretos";
        this.snackbar = true;
      }
    },
    close() {
      this.dialog = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;

  .column {
    padding: 0 5px;
  }
  .button {
    padding: 0 5px;
  }
}
</style>
