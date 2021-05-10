<template>
  <div id="app">
  
    
        <h3> Cadastro de Clientes </h3>
        <input type="text" placeholder="Seu nome" v-model="nomeField" /> <br />
        <input type="email" placeholder="Seu email" v-model="emailField" /> <br />
        <input type="number" placeholder="Sua idade" v-model="idadeField" /> <br />

        <button @click="cadastrarCliente"> Cadastrar </button>

        <hr />

    <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
      <h5> {{ index + 1 }} </h5>
      <Cliente :cliente="cliente" @meRemova="deletarCliente($event)"/>

      <hr>
    </div>

  </div>
</template>


<script>
import _ from 'lodash';
import Cliente from './components/Cliente'
//import Produto from './components/Produto'


export default {
  name: 'App',
  data() {
    return {
      nomeField: "",
      emailField: "",
      idadeField: 0,
      clientes: [
        {
          id: 1,
          nome : "Júlio César",
          email: "julio@gmail.com",
          idade: "24"
        },
        {
          id: 2,
          nome : "Thayanne Andrade",
          email: "thayanne@gmail.com",
          idade: "23"
        },
        {
          id: 3,
          nome : "Jorge Júnior",
          email: "jorge@gmail.com",
          idade: "33"
        },
      ]
    }
  },
  components: {
    Cliente,
  },
  methods: {
    cadastrarCliente: function() {

      if (this.nomeField == "" || this.nomeField == " " || this.nomeField.length == 3) {
        console.log("Digite os dados corretamente");
      } else {

      this.clientes.push({ nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now() })

      this.nomeField= "";
      this.emailField= "";
      this.idadeField= 0;
      }
    },

    deletarCliente: function($event) {
      console.log("Recebendo o evento");

      let id = $event.idDoCliente;
      let novaListaClientes = this.clientes.filter(cliente => cliente.id != id);

      this.clientes = novaListaClientes;
    }
  },
  computed: {
    orderClientes: function(){
      return _.orderBy(this.clientes, ['nome'], ['asc']); 
    }
  }
}
</script>

<style scoped>

</style>>


