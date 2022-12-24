<template>
  <div>
    <topo-componente @navegar="componente = $event"> </topo-componente>
    <conteudo-componente :conteudo="componente"></conteudo-componente>
  </div>
</template>

<script>
import ConteudoComponente from "./components/layouts/ConteudoComponente.vue";
import TopoComponente from "./components/layouts/TopoComponente.vue";

export default {
  name: "App",
  data: () => ({
    componente: "HomePage",
  }),
  components: {
    TopoComponente,
    ConteudoComponente,
  },
};
</script>

<style scoped>
</style>
