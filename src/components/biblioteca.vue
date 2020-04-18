<template>
  <div class="flex">
    <!-- Formulário -->
    <FormBiblioteca v-on:emit-comment="get" />
    <div>
      <b-table :items="items" :fields="fields" striped responsive="sm">
        <template v-slot:cell(Excluir_Livro)="row">
          <b-button
            size="sm"
            @click="apagar(items.id)"
            class="mr-2"
          >{{ row.detailsShowing ='excluir'}} livro</b-button>
        </template>
        <template v-slot:cell(Editar_Livro)="row">
          <b-button
            size="sm"
            @click="editar(items.id)"
            class="mr-2"
          >{{ row.detailsShowing ='editar'}} livro</b-button>
        </template>
      </b-table>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import FormBiblioteca from "./FormBiblioteca.vue";
export default {
  name: "biblioteca",
  components: {
    FormBiblioteca
  },
  data() {
    return {
      fields: [
        "titulo",
        "editora",
        "quantidadePaginas",
        "Excluir_Livro",
        "Editar_Livro"
      ],
      items: []
    };
  },
  methods: {
    get() {
      axios.get("http://localhost:8081/livros").then(res => {
        this.items = res.data;
      });
    },

    apagar: function(items) {
      axios
        .delete("http://localhost:8081/" + items)
        .then(resultado => {
          console.log(resultado)
        })
     
    },

    editar: function(items) {
      axios
        .put("http://localhost:8081/" + items)
        .then(resultado => {
          let indice = this.resultados.indexOf(resultado);
          this.resultados.splice(indice, 1);
          this.sucesso = "Registro editado com sucesso";
        })
        
    }
  },
  mounted() {
    this.get();
  }
};
</script>

<style>
.search {
  display: flex;
  width: 69vw;
  height: 19vh;
  align-items: center;
}
.flex {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.table {
  width: 40vw !important;
}
</style>