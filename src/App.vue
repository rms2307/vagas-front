<template>
  <div>
    <h1>Componente App</h1>
    <topo-componente> </topo-componente>
    <conteudo-componente></conteudo-componente>
  </div>
</template>

<script>
import ConteudoComponente from "./components/layouts/ConteudoComponente.vue";
import TopoComponente from "./components/layouts/TopoComponente.vue";

export default {
  name: "App",
  components: {
    TopoComponente,
    ConteudoComponente,
  },
};
</script>

<style scoped>

</style>
