<template>

  <div>
    <h1>Teste</h1>
    <form @submit.prevent="salvar()">
      <label>Nome: </label>
      <input type="text" id="nome" v-model="nome" size="30" required><br />
      <br />
      <label>Nota 1: </label>
      <input type="number" id="nota" v-model="primeira_nota" size="30" required><br />
      <label>Nota 2: </label>
      <input type="number" id="nota" v-model="segunda_nota" size="30" required><br />
      <label>Nota 3: </label>
      <input type="number" id="nota" v-model="terceira_nota" size="30" required><br />
      <input type="submit" id="send" value="Salvar" />

    </form>
    <!-------------------------------------------------------------------------------->
    <table>
      <tr>
        <th>Nome</th>
        <th>Media</th>
        <th>Situacao</th>
      </tr>

      <tr v-for="a in alunos" :key="a.situacao" @click="approved = a" 
      :class="[a.situacao]">
        <td>{{ a.nome }}</td>
        <td>{{ a.media }}</td>
        <td>{{ a.situacao }}</td>
      </tr>
    </table>
  </div>
</template>

<script>


export default {
  data() {
    return {
      approved:null,
      alunos: [
        {
          nome: "",
          media: null,
          situacao: "",
          notaUm: null,
          notaDois: null,
          notaTres: null

        }
      ],
      nome: "",
      media: null,
      situacao: "",
      notaUm: null,
      notaDois: null,
      notaTres: null
    }

  },
  methods: {
    isApproved(aluno){
      return this.approved != null && aluno.situacao == "Aprovado" 
    },
    caluloPesoDois() {
      let peso = this.alunos.notaDois = this.segunda_nota * 2
      return peso
    },
    caluloPesoTres() {
      let peso = this.alunos.notaTres = this.terceira_nota * 3
      return peso
    },
    somar() {
      this.alunos.notaUm = this.primeira_nota

      let soma = this.alunos.notaUm +
        this.caluloPesoDois() +
        this.caluloPesoTres()

      if (soma != 0)
        alert(soma)

      return soma / 6

    },
    situacaoAluno() {
      return this.somar() >= 7 ? "Aprovado" : "Reprovado";

    },
    salvar() {
      this.alunos.push({
        nome: this.nome,
        media: this.somar(),
        situacao: this.situacaoAluno(),
        notaUm: this.primeira_nota,
        notaDois: this.segunda_nota,
        notaTres: this.terceira_nota
      });
    }
  },
  coputed: {

  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.Aprovado {
  background-color: rgb(0, 191, 255);
}
.Reprovado {
  background-color: rgb(250, 11, 11);
}

</style>
