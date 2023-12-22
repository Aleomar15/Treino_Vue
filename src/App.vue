<template>
  <div id="app">
      <h1>Guia Clientes</h1>
      <h3>Cadastro: </h3>
      <small id="nomeERROR" v-show="deuErro">O nome é invalido tente novamnete!</small><br>
      <input type="text" placeholder="nome" v-model="nomeField"><br>
      <input type="text" placeholder="email" v-model="emailField"><br>
      <input type="number" placeholder="idade" v-model="idadeField"><br>
      <button @click="cadastrarUsuario" >Cadastrar</button>
      <hr>
      <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
        <h4>{{ index + 1 }}</h4>
        <ClienteItem :cliente="cliente" @meDelete="deletarUsuario($event)"/>
      </div>
      
  </div>
</template>

<script>
import _ from 'lodash';
import ClienteItem from './components/ClienteItem.vue';
//import ProdutoItem from './components/ProdutoItem.vue';

export default {
    name: 'App',
    data(){
      return{
        deuErro: false,
        nomeField:"",
        emailField:"",
        idadeField: 0,
        nomeQualquer: "Alexandre O",
        clienteV: {
          nome: "Alexandre",
          email: "teste@gmail.com",
          idade: 99
        },
        clientes: [
          {
            id: 2,
            nome: "Alexandre",
            email: "teste@gmail.com",
            idade: 99
          },
          {
            id: 3,
            nome: "Alexandre2",
            email: "teste2@gmail.com",
            idade: 45
          },
          {
            id: 4,
            nome: "Alexandre3",
            email: "teste3@gmail.com",
            idade: 35
          },
        ]
      }
    },
    components: { ClienteItem,
    //ProdutoItem 
    },
    methods: {
      cadastrarUsuario: function(){
        if(this.nomeField == " " || this.nomeField == " " || this.nomeField.length < 3){
          this.deuErro= true;
        }else{
          this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()})
          this.nomeField = "";
          this.emailField = "";
          this.idadeField = 0;
          this.deuErro = false;
        }
        
      },
      deletarUsuario: function($event){
        console.log("Recebendo evento!");
        var id = $event.idCliente;
        var novoArray = this.clientes.filter(cliente => cliente.id != id);
        this.clientes = novoArray;
      },
      
      },
      computed: {
        orderClientes: function(){
          return _.orderBy(this.clientes,['nome'],['asc']);
        }
      
    }

}
</script>

<style>

#nomeERROR{
  color: red;
}
</style>
