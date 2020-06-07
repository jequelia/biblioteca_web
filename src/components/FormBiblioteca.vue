<template>
  <div class="form">
    <div>
      <b-button id="show-btn" @click="$bvModal.show('bv-modal-example')">Cadastrar um livro</b-button>

      <b-modal id="bv-modal-example" hide-footer>
        <b-form @submit="onSubmit" @reset="onReset" v-if="show">
          <b-form-group
            id="input-group-1"
            label="Titulo do livro"
            label-for="input-1"
            description="digite o nome do livro"
          >
            <b-form-input
              id="input-1"
              v-model="form.titulo"
              type="text"
              required
              placeholder="titulo"
            ></b-form-input>
          </b-form-group>

          <b-form-group
            id="input-group-2"
            description="digite a editora do livro"
            label="Editora"
            label-for="input-2"
          >
            <b-form-input id="input-2" v-model="form.editora" required placeholder="Editora"></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-3" label="Quantidade de paginas" label-for="input-3">
            <b-form-input id="input-3" type="number" v-model="form.quantidadePaginas" required></b-form-input>
          </b-form-group>

          <b-button type="submit" variant="primary">cadastrar</b-button>
        </b-form>
      </b-modal>
    </div>
  </div>
</template>



<script>
import axios from "axios";
export default {
  name: "FormBiblioteca",
  data() {
    return {
      form: {
        titulo: "",
        editora: "",
        quantidadePaginas: ""
      },
      show: true
    };
  },

  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      axios
        .post("http://localhost:8080/livros", this.form)
        .then(res => this.$emit("emit-comment", res));
    },

    onReset(evt) {
      evt.preventDefault();
      this.form.titulo = "";
      this.form.editora = "";
      this.form.quantidadePaginas = "";
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    }
  }
};
</script>

<style>
.form {
    width: 15vw;
    box-shadow: darkslategrey;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 4%;
}
form{
  width: 24vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

</style>