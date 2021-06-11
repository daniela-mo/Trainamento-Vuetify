<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{}"> </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Cadastre-se</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Nome*"
                  color="#700343"
                  required
                  v-model="form.nome"
                />
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  label="Sobrenome"
                  required
                  v-model="form.sobrenome"
                  color="#700343"
                />
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  label="Email*"
                  required
                  color="#700343"
                  v-model="form.email"
                  prepend-inner-icon="email"
                />
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="Confirmar Email*"
                  required
                  color="#700343"
                  v-model="form.confirmaEmail"
                  prepend-inner-icon="email"
                />
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Senha*"
                  required
                  color="#700343"
                  :type="show ? 'text' : 'password'"
                  @click:append="show = !show"
                  v-model="form.senha"
                  :append-icon="show ? 'visibility' : 'visibility_off'"
                  prepend-inner-icon="lock"
                />
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  label="Confirmar Senha*"
                  required
                  color="#700343"
                  v-model="form.confirmaSenha"
                  prepend-inner-icon="lock"
                  :append-icon="showConfirm ? 'visibility' : 'visibility_off'"
                  :type="showConfirm ? 'text' : 'password'"
                  @click:append="showConfirm = !showConfirm"
                />
              </v-col>
            </v-row>

            <v-col cols="12" sm="6">
              <v-row>
                <v-radio-group v-model="form.radios" mandatory>
                  <v-radio label="Feminino" value="feminino" color="#700343" />

                  <v-radio
                    label="Masculino"
                    value="masculino"
                    color="#700343"
                  />
                </v-radio-group>
              </v-row>
            </v-col>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="#700343" class="ma-2 white--text" @click="close()">
            Fechar
          </v-btn>
          <v-btn color="#700343" outlined @click="register">
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
    show: "",
    showConfirm: "",
    form: {
      nome: "",
      sobrenome: "",
      email: "",
      confirmaEmail: "",
      senha: "",
      confirmaSenha: "",
      radios: null,
    },
  }),
  props: {
    dialog: Boolean,
    close: Function,
  },
  methods: {
    async register() {
      if (this.form.senha === this.form.confirmaSenha) {
        const data = await axios.post(" http://localhost:3000/user", {
          nome: this.form.nome,
          sobrenome: this.form.sobrenome,
          email: this.form.email,
          confirmaEmail: this.form.emailconfirmaEmail,
          senha: this.form.senha,
          confirmaSenha: this.form.confirmaSenha,
          genero: this.form.radios,
        });
        this.close();
      }
    },
  },
};
</script>
