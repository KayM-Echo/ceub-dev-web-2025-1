<template>
    <div>
        <h1>Pedidos de Tacos</h1>
        <lista-pedido-component/>
    </div>

</template>

<script>
    import ListaPedidoComponent from '@/components/ListaPedidoComponent.vue';

    export default {
        name: "PedidosView",
        components: {
            ListaPedidoComponent
        }
    }

</script>

<style scoped></style>