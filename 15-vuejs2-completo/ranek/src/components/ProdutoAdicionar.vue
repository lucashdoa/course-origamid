<template>
  <form class="adicionar-produto">
    <label for="nome">Nome</label>
    <input type="text" id="nome" name="nome" v-model="produto.nome" />
    <label for="preco">Preço (R$)</label>
    <input type="text" id="preco" name="preco" v-model="produto.preco" />
    <label for="fotos">Fotos</label>
    <input type="file" id="fotos" name="fotos" ref="fotos" />
    <label for="descricao">Descrição</label>
    <textarea id="descricao" name="descricao" v-model="produto.descricao" />
    <input
      type="button"
      class="btn"
      value="Adicionar Produto"
      @click.prevent="adicionarProduto"
    />
  </form>
</template>

<script>
import { api } from "@/services.js";
export default {
  data() {
    return {
      produto: {
        nome: "",
        preco: " ",
        descricao: "",
        fotos: null,
        vendido: "false",
      },
    };
  },
  methods: {
    adicionarProduto() {
      this.formatarProduto();
      api.post("/produto", this.produto).then(() => {
        this.$store.dispatch("getUsuarioProdutos");
      });
    },
    formatarProduto() {
      this.produto.usuario_id = this.$store.state.usuario.id;
    },
  },
};
</script>

<style scoped>
.adicionar-produto {
  display: grid;
  grid-template-columns: 100px 1fr;
  align-items: center;
  margin-bottom: 60px;
}

.btn {
  grid-column: 2;
}
</style>
