<template>
    <div :class="{'cliente' : !isPremium, 'cliente-premium' : isPremium}">
        <h4> Nome : {{ cliente.nome }} </h4>
        <hr />
        <p>Email: {{ cliente.email | processarEmail }} </p>
        <hr />
        <p v-show="showAge === true ">Idade: {{ cliente.idade }} </p>

        <button @click="mudarCor"> Mudar cor </button>
        <button @click="emitirEventoDelete"> Apagar Cliente </button>
    </div>
</template>

<script>

export default {
    data() {
        return {
           isPremium: false
        }
    },
    props: {
        cliente: Object,
        showAge: Boolean
    },
    methods: {
            mudarCor: function(){
                this.isPremium = !this.isPremium;
            },
            emitirEventoDelete: function() {
                console.log("Emitindo do filho");
                this.$emit("meRemova", { idDoCliente: this.cliente.id, component: this});
            }
        },
    filters: {
        processarEmail: function(value) {
            return value.toUpperCase();
        }
    }
    }

</script>

<style scoped>
    
    .cliente {
        background-color: #9fd8ff;
        font-family: 'Courier New', Courier, monospace;
        font-weight: 600;
        max-width: 600px;
        border-radius: 10px;
        margin-bottom: 2%;
        padding: 5% 5%;
    }

    .cliente-premium {
        background-color: 	#9F9F9F;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        font-weight: 600;
        max-width: 600px;
        border-radius: 10px;
        margin-bottom: 2%;
        padding: 5% 5%;
    }   
</style>
