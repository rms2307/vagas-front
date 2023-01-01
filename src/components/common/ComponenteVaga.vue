<template>
  <div class="card">
    <div class="card-header bg-dark text-white">
      <div class="col d-flex justify-content-between">
        <div>
          {{ titulo }}
        </div>
        <div>
          <div class="form-check form-switch">
            <input
              type="checkbox"
              class="form-check-input"
              @click="toggleVagaFavorita()"
              v-model="favoritada"
            />
            <label for="" class="form-check-label">Favoritar</label>
          </div>
        </div>
      </div>
    </div>
    <div class="card-body">
      <p>{{ descricao }}</p>
    </div>
    <div class="card-footer">
      <small class="text-muted">
        Salário: R$ {{ salario }} | Modalidade: {{ getModalidade }} | Tipo:
        {{ getTipo }} | Publicação:
        {{ getPublicacao }}
      </small>
    </div>
  </div>
</template>

<script>
export default {
  name: "ComponenteVaga",
  data: () => ({
    favoritada: false,
  }),
  props: {
    titulo: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    descricao: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    salario: {
      type: Number,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    modalidade: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    tipo: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 0) return false;
        return true;
      },
    },
    publicacao: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
  },
  methods: {
    verificarSeVagaFavorita() {
      let vagas = JSON.parse(localStorage.getItem("vagasFavoritas"));
      if (!vagas) return;

      let indiceArray = vagas.indexOf(this.titulo);
      if (indiceArray !== -1) return true;
      return false;
    },
    toggleVagaFavorita() {
      this.favoritada = !this.favoritada;
      if (this.favoritada) {
        this.emitter.emit("favoritarVaga", this.titulo);
      } else {
        this.emitter.emit("desfavoritarVaga", this.titulo);
      }
    },
  },
  computed: {
    getModalidade() {
      switch (this.modalidade) {
        case "1":
          return "Home Office";
        case "2":
          return "Presencial";
      }
      return "";
    },
    getTipo() {
      switch (this.tipo) {
        case "1":
          return "CLT";
        case "2":
          return "PJ";
      }
      return "";
    },
    getPublicacao() {
      let dataPublicacao = new Date(this.publicacao);
      return dataPublicacao.toLocaleDateString("pt-BR");
    },
  },
  mounted() {
    this.favoritada = this.verificarSeVagaFavorita();
  },
};
</script>
