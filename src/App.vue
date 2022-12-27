<template>
  <div>
    <componente-vagas-favoritas />
    <componente-topo @navegar="componente = $event" />
    <componente-alerta v-if="exibirAlerta">
      <template v-slot:titulo>
        <h5>{{ alerta.titulo }}</h5>
      </template>
      <p>{{alerta.descricao}}</p>
    </componente-alerta>
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
    alerta: { titulo: "", descricao: "" },
  }),
  components: {
    ComponenteTopo,
    ComponenteConteudo,
    ComponenteVagasFavoritas,
    ComponenteAlerta,
  },
  mounted() {
    this.emitter.on("alerta", (value) => {
      this.exibirAlerta = true;
      this.alerta = value;
      setTimeout(() => (this.exibirAlerta = false), 4000);
    });
  },
};
</script>