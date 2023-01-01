<template>
  <div>
    <div class="divVagasFavoritas">
      <button
        class="btn btn-primary"
        type="button"
        data-bs-toggle="offcanvas"
        data-bs-target="#offcanvasScrolling"
        aria-controls="offcanvasScrolling"
      >
        Vagas Favoritas
      </button>
    </div>

    <div
      class="offcanvas offcanvas-end"
      data-bs-scroll="true"
      data-bs-backdrop="false"
      tabindex="-1"
      id="offcanvasScrolling"
      aria-labelledby="offcanvasScrollingLabel"
    >
      <div class="offcanvas-header">
        <h5 class="offcanvas-title" id="offcanvasScrollingLabel">
          Vagas Favoritadas
        </h5>
        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="offcanvas"
          aria-label="Close"
        ></button>
      </div>
      <div class="offcanvas-body">
        <ul class="list-group">
          <li
            class="list-group-item"
            v-for="(vaga, index) in vagas"
            :key="index"
          >
            {{ vaga }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ComponenteVagasFavoritas",
  data: () => ({
    vagas: [],
  }),
  methods: {
    getVagasFavoritas() {
      this.vagas = JSON.parse(localStorage.getItem("vagasFavoritas"));
    },
    favoritarVaga(vagaFavoritada) {      
      if (!this.vagas) this.vagas = [];
      this.vagas.push(vagaFavoritada);

      localStorage.setItem("vagasFavoritas", JSON.stringify(this.vagas));
    },
    desfavoritarVaga(vagaDesfavoritada) {
      let indiceArray = this.vagas.indexOf(vagaDesfavoritada);
      if (indiceArray !== -1) this.vagas.splice(indiceArray, 1);

      localStorage.setItem("vagasFavoritas", JSON.stringify(this.vagas));
    },
  },
  mounted() {
    this.getVagasFavoritas();

    this.emitter.on("favoritarVaga", (vaga) => {
      this.favoritarVaga(vaga);
    });

    this.emitter.on("desfavoritarVaga", (vaga) => {
      this.desfavoritarVaga(vaga);
    });
  },
};
</script>

<style scoped>
.divVagasFavoritas {
  position: absolute;
  z-index: 1;
  top: 70px;
  right: 0px;
}
</style>