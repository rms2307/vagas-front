<template>
  <div class="container py-4">
    <div class="row">
      <div class="col">
        <componente-pesquisar-vaga />
      </div>
    </div>
    <componente-lista-vagas />

    <div class="row mt-5">
      <div class="col-4">
        <componente-indicador-vaga
          titulo="Vagas abertas"
          :indicador="quantidadeVagas"
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
    quantidadeVagas: 0,
  }),
  methods: {
    getUsuariosOnline() {
      this.usuariosOnline = Math.floor(Math.random() * 101);
    },
    getQuantidadeDeVagas() {
      this.emitter.on("atualizarQuantidadeVagas", (qtd) => {
        this.quantidadeVagas = qtd;
      });
    },
  },
  created() {
    setInterval(this.getUsuariosOnline, 1000);
    this.getQuantidadeDeVagas();
  },
};
</script>