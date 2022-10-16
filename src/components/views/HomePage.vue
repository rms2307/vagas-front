<template>
  <div class="container py-4">
    <div class="row">
      <div class="col">
        <pesquisar-vaga></pesquisar-vaga>
      </div>
    </div>

    <div class="row mt-5">
      <div class="col-4">
        <indicador-vaga
          titulo="Vagas abertas"
          indicador="100"
          bg="bg-dark"
          color="text-white"
        ></indicador-vaga>
      </div>
      <div class="col-4">
        <indicador-vaga
          titulo="Profissionais cadastrados"
          indicador="220"
          bg="bg-dark"
          color="text-white"
        ></indicador-vaga>
      </div>
      <div class="col-4">
        <indicador-vaga
          titulo="Visitantes online"
          :indicador="usuariosOnline"
          bg="bg-ligth"
          color="text-dark"
        ></indicador-vaga>
      </div>
    </div>
  </div>
</template>

<script>
import IndicadorVaga from "../common/IndicadorVaga.vue";
import PesquisarVaga from "../common/PesquisarVaga.vue";

export default {
  name: "HomePage",
  components: {
    PesquisarVaga,
    IndicadorVaga,
  },
  data: () => ({
    usuariosOnline: 0,
  }),
  methods: {
    getUsuariosOnline() {
      this.usuariosOnline = Math.floor(Math.random() * 101);
    },
  },
  created() {
    setInterval(this.getUsuariosOnline, 1000);
  },
};
</script>