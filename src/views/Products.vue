<template>
  <v-container>
    <v-row>
      <v-col>

        <v-text-field label="id" v-model="product.id"></v-text-field>

        <v-text-field label="nome" v-model="product.name"></v-text-field>
        <v-btn @click="editarProduto">Salvar</v-btn>

        <v-btn @click="cadastrarProduto">Cadastrar</v-btn> 

        <v-btn @click="buscarProdutos">Buscar</v-btn>
        <v-data-table
          :headers="headers"
          :items="produtos"
          @click:row="editProduto"
          :items-per-page="5"
          class="elevation-1"
        >
          <template v-slot:item.actions="{ item }">
            <v-icon @click="deletarProduto(item.id)"> mdi-delete </v-icon>
          </template>

        </v-data-table>
      </v-col>
    </v-row>
  </v-container>
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
        { text: "Actions", value: "actions", sortable: false },
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
    deletarProduto(id) {
      axios.delete("http://localhost:3000/products/" + id).then(() => {
        this.buscarProdutos();
        alert("produto deletado com sucesso");
      });
    },
    editarProduto() {
      axios
        .patch(
          "http://localhost:3000/products/" + this.product.id,
          this.product
        )
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