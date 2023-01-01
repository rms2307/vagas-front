<template>
  <div class="row mt-5" v-for="(vaga, index) in vagas" :key="index">
    <div class="col">
      <componente-vaga v-bind="vaga" />
    </div>
  </div>
</template>

<script>
import ComponenteVaga from "../common/ComponenteVaga.vue";

export default {
  name: "ComponenteListaVagas",
  data: () => ({
    vagas: [],
  }),
  components: {
    ComponenteVaga,
  },
  methods: {
    filtrarVagas() {
      this.emitter.on("filtrarVagas", (input) => {
        const vagas = JSON.parse(localStorage.getItem("vagas"));
        this.vagas = vagas.filter((v) =>
          v.titulo.toLowerCase().includes(input.titulo.toLowerCase())
        );
      });
    },
  },
  mounted() {
    this.vagas = JSON.parse(localStorage.getItem("vagas"));
    this.quantidadeVagasAbertas = this.vagas.length;

    this.filtrarVagas();
  },
};
</script>