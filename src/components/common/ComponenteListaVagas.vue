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
    quantidadeVagas: 0,
  }),
  components: {
    ComponenteVaga,
  },
  methods: {
    filtrarVagas() {
      this.emitter.on("filtrarVagas", (input) => {
        const vagas = JSON.parse(localStorage.getItem("vagas"));
        if (!vagas) return;

        this.vagas = vagas.filter(
          (v) =>
            v.titulo.toLowerCase().includes(input.toLowerCase()) ||
            v.descricao.toLowerCase().includes(input.toLowerCase())
        );
      });
    },
  },
  mounted() {
    this.vagas = JSON.parse(localStorage.getItem("vagas"));
    if (this.vagas) this.quantidadeVagas = this.vagas.length;

    this.filtrarVagas();
    this.emitter.emit("atualizarQuantidadeVagas", this.quantidadeVagas);
  },
};
</script>