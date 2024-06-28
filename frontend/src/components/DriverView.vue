<template>
    <div class="container mt-5">
        <h1 class="text-center text-white">Bienvenido Conductor</h1>
        <p class="text-center text-white">Conéctate y empieza a recibir solicitudes de viaje.</p>
        <div class="row justify-content-center">
            <button class="btn btn-primary btn-lg mr-3">Conectarse</button>
            <button class="btn btn-secondary btn-lg">Ver Historial</button>
        </div>
        <div class="row justify-content-center mt-3">
            <button class="btn btn-danger btn-lg" @click="goBack">Regresar</button>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        goBack() {
            this.$emit('view-change', 'main');
        }
    }
};
</script>

<style scoped>
body {
    background-color: #333;
    color: #fff;
}
</style>