<template>
    <div :class="{'cliente': !isPremium,'cliente-premium': isPremium }">
        <h4>Nome: {{ cliente.nome }}</h4>
        <hr>
        <p>Email: {{ cliente.email}}</p>
        <p v-if="showIdade === true">  Idade: {{ cliente.idade }}</p>
        <p v-else>O usuario escondeu a idade</p>
        <button @click="mudarCor($event)">Mudar cor!</button>
        <button @click="emitirEventoDelete">Deletar</button>
        <h4>Id especial: {{ idEspecial }}</h4>
    </div>
</template>

<script>

export default {
    data(){
        return {
            isPremium: false
        }
    },
    props: {
        cliente: Object,
        showIdade: Boolean
    },
    methods: {
        mudarCor: function($event){
            console.log($event)
            this.isPremium = !this.isPremium;
        },
        emitirEventoDelete: function(){
            console.log("Emitindo evento filho")
            this.$emit("meDelete",{idCliente: this.cliente.id,curso: "Formação Node.js",emPromocao: true, component: this});
        },
        testar: function(){
        console.log("Testando para valer");
        alert("Isso é um alert");
      }
    },
    /*filters:{
        processarEmail: function(value){
            return value.toUpperCase();
        }
    }*/
    computed: {
        idEspecial: function(){
            return(this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
    }
}
</script>

<style scoped>
    .cliente{
        background-color: #ECE5E3;
        max-width: 600px;
        height: 180px;
        padding: 1%;
        margin-top: 2%;
    }

    .cliente-premium{
        background-color: black;
        color: yellow;
        max-width: 600px;
        height: 180px;
        padding: 1%;
        margin-top: 2%;
    }
</style>
