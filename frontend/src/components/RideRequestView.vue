<template>
    <div class="container mt-5">
        <h1 class="text-center text-white">Esperando Conductor</h1>
        <p class="text-center text-white">Tu solicitud ha sido enviada. Espera mientras encontramos un conductor.</p>
        <div class="row justify-content-center mt-3">
            <button class="btn btn-danger btn-lg" @click="cancelRide">Cancelar Viaje</button>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        cancelRide() {
            this.$emit('view-change', 'customer');
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