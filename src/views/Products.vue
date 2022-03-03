<template>
  <div>
    <v-text-field label="id" readonly v-model="product.id"></v-text-field>
    <v-text-field label="nome" v-model="product.name"></v-text-field>
    <v-btn @click="editarProduto">Salvar</v-btn>
    <v-btn @click="buscarProdutos">Buscar</v-btn>
    <v-data-table
      :headers="headers"
      :items="produtos"
      @click:row="editProduto"
      :items-per-page="5"
      class="elevation-1"
    ></v-data-table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      produtos: [],
      product: {},
      headers: [
        { text: "ID", value: "id" },
        { text: "Nome", value: "name" },
      ],
    };
  },
  methods: {
    buscarProdutos() {
      axios
        .get("http://localhost:3000/products")
        .then((response) => {
          this.produtos = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    editarProduto() {
      axios
        .put("http://localhost:3000/products/" + this.product.id, this.product)
        .then((response) => {
          console.log(response);
          this.buscarProdutos();
        })
        .catch((error) => {
          console.log(error);
        });
    },

    editProduto(item) {
      console.log(item);
      this.product = item;
    },
    cadastrarProduto() {
      axios.post("http://localhost:3000/products", this.product).then((res) => {
        console.log(res);
        alert("Produto cadastrado com sucesso!");
      });
    },
  },
};
</script>