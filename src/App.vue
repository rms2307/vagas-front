<template>
  <div>
    <componente-vagas-favoritas />
    <componente-topo @navegar="componente = $event" />
    <componente-alerta v-if="alertaVisivel">
      <template v-slot:titulo>
        <h5>{{ alerta.titulo }}</h5>
      </template>
      <p>{{ alerta.descricao }}</p>
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
    alertaVisivel: false,
    alerta: { titulo: "", descricao: "" },
  }),
  components: {
    ComponenteTopo,
    ComponenteConteudo,
    ComponenteVagasFavoritas,
    ComponenteAlerta,
  },
  methods: {
    exibirAlerta() {
      this.emitter.on("alerta", (value) => {
        this.alertaVisivel = true;
        this.alerta = value;
        setTimeout(() => (this.alertaVisivel = false), 4000);
      });
    },
  },
  mounted() {
    this.exibirAlerta();
  },
};
</script>