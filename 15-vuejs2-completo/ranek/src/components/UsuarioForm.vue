<template>
  <form>
    <div v-if="mostrarDadosLogin" class="usuario">
      <label for="nome">Nome</label>
      <input v-model="nome" type="text" name="nome" id="nome" />
      <label for="email">Email</label>
      <input v-model="email" type="email" name="email" id="email" />
      <label for="senha">Senha</label>
      <input v-model="senha" type="password" name="senha" id="senha" />
    </div>
    <label for="cep">CEP</label>
    <input
      v-model="cep"
      type="text"
      name="cep"
      id="cep"
      @keyup="preencherCEP"
    />
    <label for="rua">Rua</label>
    <input v-model="rua" type="text" name="rua" id="rua" />
    <label for="numero">Numero</label>
    <input v-model="numero" type="text" name="numero" id="numero" />
    <label for="bairro">Bairro</label>
    <input v-model="bairro" type="text" name="bairro" id="bairro" />
    <label for="cidade">Cidade</label>
    <input v-model="cidade" type="text" name="cidade" id="cidade" />
    <label for="estado">Estado</label>
    <input v-model="estado" type="text" name="estado" id="estado" />
    <div class="button">
      <slot></slot>
    </div>
  </form>
</template>

<script>
import { getCEP } from "@/services.js";
export default {
  methods: {
    preencherCEP() {
      const CEP = this.cep.replace(/\D/g, "");
      if (CEP.length === 8) {
        getCEP(CEP).then((response) => {
          console.log(response);
          this.rua = response.data.logradouro;
          this.bairro = response.data.bairro;
          this.cidade = response.data.localidade;
          this.estado = response.data.uf;
        });
      }
    },
  },
  computed: {
    nome: {
      get() {
        return this.$store.state.usuario.nome;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { nome: value });
      },
    },
    email: {
      get() {
        return this.$store.state.usuario.email;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { email: value });
      },
    },
    senha: {
      get() {
        return this.$store.state.usuario.senha;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { senha: value });
      },
    },
    cep: {
      get() {
        return this.$store.state.usuario.cep;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { cep: value });
      },
    },
    rua: {
      get() {
        return this.$store.state.usuario.rua;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { rua: value });
      },
    },
    numero: {
      get() {
        return this.$store.state.usuario.numero;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { numero: value });
      },
    },
    bairro: {
      get() {
        return this.$store.state.usuario.bairro;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { bairro: value });
      },
    },
    cidade: {
      get() {
        return this.$store.state.usuario.cidade;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { cidade: value });
      },
    },
    estado: {
      get() {
        return this.$store.state.usuario.estado;
      },
      set(value) {
        this.$store.commit("UPDATE_USUARIO", { estado: value });
      },
    },
    mostrarDadosLogin() {
      return !this.$store.state.login || this.$route.name === "Usuario-editar";
    },
  },
};
</script>

<style scoped>
form,
.usuario {
  display: grid;
  grid-template-columns: 80px 1fr;
  align-items: center;
}

.usuario {
  grid-column: 1 / 3;
}

.button {
  grid-column: 2;
  margin-top: 10px;
}
</style>
