<template>
  <div>
    <componente-vagas-favoritas />
    <componente-topo @navegar="componente = $event" />
    <componente-conteudo :conteudo="componente" />
  </div>
</template>

<script>
import ComponenteVagasFavoritas from "./components/common/ComponenteVagasFavoritas.vue";
import ComponenteConteudo from "./components/layouts/ComponenteConteudo.vue";
import ComponenteTopo from "./components/layouts/ComponenteTopo.vue";

export default {
  name: "App",
  data: () => ({
    componente: "HomePage",
  }),
  components: {
    ComponenteTopo,
    ComponenteConteudo,
    ComponenteVagasFavoritas,
  },
};
</script>