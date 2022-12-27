<template>
  <div>
    <componente-vagas-favoritas />
    <componente-topo @navegar="componente = $event" />
    <componente-alerta v-if="exibirAlerta" />
    <componente-conteudo :conteudo="componente" />
  </div>
</template>

<script>
import ComponenteAlerta from "./components/common/ComponenteAlerta.vue";
import ComponenteVagasFavoritas from "./components/common/ComponenteVagasFavoritas.vue";
import ComponenteConteudo from "./components/layouts/ComponenteConteudo.vue";
import ComponenteTopo from "./components/layouts/ComponenteTopo.vue";

export default {
  name: "App",
  data: () => ({
    componente: "HomePage",
    exibirAlerta: false,
  }),
  components: {
    ComponenteTopo,
    ComponenteConteudo,
    ComponenteVagasFavoritas,
    ComponenteAlerta,
  },
  mounted() {
    this.emitter.on("alerta", () => {
      this.exibirAlerta = true;
      setTimeout(() => (this.exibirAlerta = false), 2000);
    });
  },
};
</script>