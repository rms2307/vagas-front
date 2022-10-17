<template>
  <div class="card">
    <div class="card-header bg-dark text-white">{{ titulo }}</div>
    <div class="card-body">
      <p>{{ descricao }}</p>
    </div>
    <div class="card-footer">
      <small class="text-muted">
        Salário: R$ {{ salario }} | Modalidade: {{ modalidade }} | Tipo:
        {{ tipo }} | Publicação:
        {{ publicacao }}
      </small>
    </div>
  </div>
</template>

<script>
export default {
  name: "VagaApp",
  // props: ["titulo", "descricao", "salario", "modalidade", "tipo", "publicacao"],
  props: {
    titulo: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    descricao: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    salario: {
      type: Number,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    modalidade: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
    tipo: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 0) return false;
        return true;
      },
    },
    publicacao: {
      type: String,
      required: true,
      validator(p) {
        if (p.length < 5) return false;
        return true;
      },
    },
  },
};
</script>
