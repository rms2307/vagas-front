<template>
  <div>
    <topo-padrao> </topo-padrao>
    <Conteudo></Conteudo>
  </div>
</template>

<script>
import Conteudo from "./components/layouts/ConteudoApp.vue";
import TopoPadrao from "./components/layouts/TopoPadrao.vue";

export default {
  name: "App",
  components: {
    Conteudo,
    TopoPadrao,
  },
};
</script>

<style>
#app {}
</style>
