<template>
<div id="card-content" v-for="hotDog in listaMenuHotDogs" :key="hotDog.id">
  <div id="card-linha">
    <div class="foto-hotdog">
      <img :src="hotDog.foto" :alt="hotDog.nome">
    </div>
    <div class="card-coluna">
      <p id="nome-content">{{ hotDog.nome }}</p>
      <p id="preco-content">R$ {{ hotDog.valor}},00</p>
      <p id="descricao-content">{{ hotDog.descricao }}</p>
      <button @click="selecionarHotDog(hotDog)">Selecionar</button>
    </div>
  </div>
</div>
</template>

<script>
    export default {
        name : "MenuView",
        data() {
            return {
                listaMenuHotDogs: []
            };
        },
        methods: {
            async consultarMenu() {
                const response = await fetch("http://localhost:3000/menu");
                const dados = await response.json();
                this.listaMenuHotDogs = dados.hot_dogs;
                console.log(this.listaMenuHotDogs);
            },
            selecionarHotDog(hotDogSelecionado) {
                const param = JSON.stringify(hotDogSelecionado);
                const hotDogJson = encodeURIComponent(param);
                this.$router.push({path: '/config-pedido', query: {hotDog : hotDogJson}});
            }
        },
        mounted() {
            this.consultarMenu();
        }
    }
</script>

<style scoped>

    #card-content {
        display: inline-block;
        width: 280px;
        min-height: 500px;
        margin: 20px;
        border: 1px solid #ddd;
        border-radius: 10px;
        overflow: hidden;
        box-shadow: 0 4px 8px #444;
        position: relative;
    }


    #scroll-horizontal{
        flex: 1;
        overflow-x: auto;
        white-space: nowrap;
        width: 700px;
        margin: 0 auto;
        box-shadow: inset -10px 0px 15px -20px grey;
    }

    .foto-hotdog{
    width: 100%;
    height: 200px; /* altura fixa */
    overflow: hidden;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    }

    .foto-hotdog img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 0; /* sem arredondamento aqui, já está no container */
    }

    #nome-content{
        font-size: 30px;
        font-weight: bold;
        text-align: center;
        width: 100%;
        margin: 12px;
    }

     #preco-content{
        font-size: 35px;
        font-weight: bold;
        text-align: center;
        width: 100%;
        color: yellowgreen;
    }

     #descricao-content{
        font-size: 16px;
        text-align: left;
        color: gray;
        margin: 16px;
        white-space: pre-line;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 6; /* números de linha para cortar */
        -webkit-box-orient: vertical;
    }

    .card-coluna p {
        margin: 0;
    }

    .card-coluna button {
        margin-top: auto;
        padding: 10px;
        background-color: rgb(149, 211, 90);
        color: darkslategrey;
        font-weight: bold;
        border-radius: 5px;
        border: none;
        font-size: 14px;
        width: 100%;
        transition: 0.5s;
        cursor: pointer;
    }
    .card-coluna button:hover {
        background-color: transparent;
        color: darkslategrey;
        border: solid 1px rgb(149, 211, 90);
        border-radius: 5px;
    }

    .card-linha{
        display: flex;
        flex-direction: row;
        height: 100%;
    }

    .card-coluna{
        flex-grow: 1;
        padding: 15px;
        height: 100%;
    }

</style>