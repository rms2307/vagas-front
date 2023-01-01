<template>
  <div class="row mt-5" v-for="(vaga, index) in vagas" :key="index">
    <div class="col">
      <componente-vaga v-bind="vaga" />
    </div>
  </div>
</template>

<script>
import ComponenteVaga from "../common/ComponenteVaga.vue";

export default {
  name: "ComponenteListaVagas",
  props: { vagas: Array },
  components: {
    ComponenteVaga,
  },
};
</script>