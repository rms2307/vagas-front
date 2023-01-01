<template>
  <div class="row">
    <div class="col">
      <div class="h-100 p-5 bg-light border rouded-3">
        <h2>Pesquisar Vagas</h2>
        <div class="row">
          <div class="col">
            <div class="form-group">
              <label>Título da Vaga</label>
              <input
                type="text"
                class="form-control"
                placeholder="Pesquise por palavras chaves..."
                v-model="titulo"
              />
              <small class="form-text text-muted"
                >Informe palavras que estejam relacionadas com o tipo de vaga
                que você procura.</small
              >
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <button
              class="btn btn-outline-dark mt-2"
              type="button"
              @click="pesquisarVaga()"
            >
              Buscar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ComponentePesquisarVaga",
  data: () => ({
    titulo: "",
  }),
  methods: {
    pesquisarVaga() {
      this.emitter.emit("filtrarVagas", { titulo: this.titulo });
    },
  },
};
</script>
