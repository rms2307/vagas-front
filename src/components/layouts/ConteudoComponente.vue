<template>
  <div>
    <component :is="conteudo" />
  </div>
</template>

<script>
import HomePage from "../views/HomePage.vue";
import PublicarVagaPage from "../views/PublicarVagaPage.vue";
export default {
  name: "ConteudoComponente",
  props: {
    conteudo: {
      type: String,
      required: true,
    },
  },
  components: {
    HomePage,
    PublicarVagaPage,
  }
};
</script>