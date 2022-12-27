<template>
  <div class="container py-4">
    <div class="row">
      <div class="col">
        <componente-pesquisar-vaga />
      </div>
    </div>

    <div class="row mt-5" v-for="(vaga, index) in vagas" :key="index">
      <div class="col">
        <!-- <vaga-app
          :titulo="vaga.titulo"
          :descricao="vaga.descricao"
          :salario="vaga.salario"
          :modalidade="vaga.modalidade"
          :tipo="vaga.tipo"
          :publicacao="vaga.publicacao"
        /> -->
        <componente-vaga v-bind="vaga" />
      </div>
    </div>

    <div class="row mt-5">
      <div class="col-4">
        <componente-indicador-vaga
          titulo="Vagas abertas"
          :indicador="vagasAbertas"
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
import ComponenteVaga from "../common/ComponenteVaga.vue";

export default {
  name: "HomePage",
  components: {
    ComponenteIndicadorVaga,
    ComponentePesquisarVaga,
    ComponenteVaga,
  },
  data: () => ({
    usuariosOnline: 0,
    vagasAbertas: 0,
    vagas: [],
  }),
  methods: {
    getUsuariosOnline() {
      this.usuariosOnline = Math.floor(Math.random() * 101);
    },
  },
  created() {
    setInterval(this.getUsuariosOnline, 1000);
  },
  mounted() {
    this.vagas = JSON.parse(localStorage.getItem("vagas"));
    this.vagasAbertas = this.vagas.length;
  },
};
</script>