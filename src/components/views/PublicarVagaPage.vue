<template>
  <div class="container py-4">
    <div class="row">
      <div class="col">
        <h4>Apresente a sua vaga para milhares de profissionais e de graça</h4>
      </div>
    </div>

    <div class="row mt-3">
      <div class="col">
        <label class="form-label">Título da Vaga</label>
        <input type="text" class="form-control" v-model="titulo" />
        <div class="form-text">
          Por exemplo: Programador JavaScript e VuaJS.
        </div>
      </div>
    </div>

    <div class="row mt-3">
      <div class="col">
        <label class="form-label">Descrição</label>
        <textarea type="text" class="form-control" v-model="descricao" />
        <div class="form-text">Informe os detalhes da vaga.</div>
      </div>
    </div>

    <div class="row mt-3">
      <div class="col">
        <label class="form-label">Salário</label>
        <input type="number" class="form-control" v-model="salario" />
        <div class="form-text">Informe o salário.</div>
      </div>

      <div class="col">
        <label class="form-label">Modalidade</label>
        <select class="form-select" v-model="modalidade">
          <option value="" disabled>Selecione...</option>
          <option value="1">Home Office</option>
          <option value="2">Presencial</option>
        </select>
        <div class="form-text">
          Informe onde as atividades serão realizadas.
        </div>
      </div>
      <div class="col">
        <label class="form-label">Tipo</label>
        <select class="form-select" v-model="tipo">
          <option value="" disabled>Selecione...</option>
          <option value="1">CLT</option>
          <option value="2">PJ</option>
        </select>
        <div class="form-text">Informe o tipo de contratação.</div>
      </div>
    </div>

    <div class="row mt-3">
      <div class="col">
        <button type="submit" class="btn btn-primary" @click="salvarVaga()">
          Cadastrar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PublicarVagaPage",
  data: () => ({
    titulo: "",
    descricao: "",
    salario: "",
    modalidade: "",
    tipo: "",
  }),
  methods: {
    salvarVaga() {
      let vagas = JSON.parse(localStorage.getItem("vagas"));
      if (!vagas) vagas = [];

      vagas.push({
        titulo: this.titulo,
        descricao: this.descricao,
        salario: this.salario,
        modalidade: this.modalidade,
        tipo: this.tipo,
        publicacao: this.getDataPublicacao(),
      });

      const resultadoValidarFormulario = this.validarFormulario();
      if (resultadoValidarFormulario.valido) {
        localStorage.setItem("vagas", JSON.stringify(vagas));

        this.emitirEventoAlerta(
          `sucesso`,
          `A vaga ${this.titulo} foi cadastrada com sucesso!`,
          `Parabéns, a vaga foi cadastrada e poderá ser consultada por diversos profissionais!`
        );

        this.limparFormulario();
      } else {
        this.emitirEventoAlerta(
          `erro`,
          `Erro ao cadastrar vaga!`,
          `O campo ${resultadoValidarFormulario.campo} é obrigatorio!`
        );
      }
    },
    limparFormulario() {
      this.titulo = "";
      this.descricao = "";
      this.salario = "";
      this.modalidade = 0;
      this.tipo = 0;
    },
    getDataPublicacao() {
      let tempoDecorrido = Date.now();
      let dataAtual = new Date(tempoDecorrido);
      return dataAtual.toISOString();
    },
    emitirEventoAlerta(tipo, titulo, descricao) {
      this.emitter.emit("alerta", {
        tipo: tipo,
        titulo: titulo,
        descricao: descricao,
      });
    },
    validarFormulario() {
      let resultado = { valido: true, campo: "" };

      if (this.titulo === "")
        return (resultado = { valido: false, campo: "título" });
      if (this.descricao === "")
        return (resultado = { valido: false, campo: "descrição" });
      if (this.salario === "")
        return (resultado = { valido: false, campo: "salário" });
      if (this.modalidade === "")
        return (resultado = { valido: false, campo: "modalidade" });
      if (this.tipo === "")
        return (resultado = { valido: false, campo: "tipo" });

      return resultado;
    },
  },
};
</script>