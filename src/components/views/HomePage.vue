<template>
  <div class="container py-4">
    <div class="row">
      <div class="col">
        <componente-pesquisar-vaga />
      </div>
    </div>
    <componente-lista-vagas :vagas="vagas" />

    <div class="row mt-5">
      <div class="col-4">
        <componente-indicador-vaga
          titulo="Vagas abertas"
          :indicador="quantidadeVagasAbertas"
          bg="bg-dark"
          color="text-white"
        />
      </div>
      <div class="col-4">
        <componente-indicador-vaga
          titulo="Profissionais cadastrados"
          indicador="220"
          bg="bg-dark"
          color="text-white"
        />
      </div>
      <div class="col-4">
        <componente-indicador-vaga
          titulo="Visitantes online"
          :indicador="usuariosOnline"
          bg="bg-ligth"
          color="text-dark"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ComponenteIndicadorVaga from "../common/ComponenteIndicadorVaga.vue";
import ComponentePesquisarVaga from "../common/ComponentePesquisarVaga.vue";
import ComponenteListaVagas from "../common/ComponenteListaVagas.vue";

export default {
  name: "HomePage",
  components: {
    ComponenteIndicadorVaga,
    ComponentePesquisarVaga,
    ComponenteListaVagas,
  },
  data: () => ({
    usuariosOnline: 0,
    quantidadeVagasAbertas: 0,
    vagas: [],
  }),
  methods: {
    getUsuariosOnline() {
      this.usuariosOnline = Math.floor(Math.random() * 101);
    },
    filtrarVagas() {
      this.emitter.on("filtrarVagas", (input) => {
        const vagas = JSON.parse(localStorage.getItem("vagas"));
        this.vagas = vagas.filter((v) =>
          v.titulo.toLowerCase().includes(input.titulo.toLowerCase())
        );
      });
    },
  },
  created() {
    setInterval(this.getUsuariosOnline, 1000);
  },
  mounted() {
    this.vagas = JSON.parse(localStorage.getItem("vagas"));
    this.quantidadeVagasAbertas = this.vagas.length;

    this.filtrarVagas();
  },
};
</script>