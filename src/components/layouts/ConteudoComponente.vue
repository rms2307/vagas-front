<template>
  <div>
    <h1>Componente Conteudo</h1>
    <button @click="conteudo = 'home-page'">Home</button>
    <button @click="conteudo = 'publicar-vaga-page'">Publicar Vaga</button>
    <!-- <home-page></home-page>
    <publicar-vaga-page></publicar-vaga-page> -->
    <component :is="conteudo" />
  </div>
</template>

<script>
import HomePage from "../views/HomePage.vue";
import PublicarVagaPage from "../views/PublicarVagaPage.vue";
export default {
  name: "ConteudoComponente",
  components: {
    HomePage,
    PublicarVagaPage,
  },
  data: () => ({
    conteudo: "home-page",
  }),
};
</script>

<style scoped>
</style>