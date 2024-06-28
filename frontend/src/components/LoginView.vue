<template>
    <div class="container mt-5">
        <h1 class="text-center text-white">Iniciar Sesión</h1>
        <form class="text-left mt-4">
            <div class="form-group">
                <label for="username">Nombre de Usuario</label>
                <input type="text" class="form-control" id="username" placeholder="Ingresa tu nombre de usuario">
            </div>
            <div class="form-group">
                <label for="password">Contraseña</label>
                <input type="password" class="form-control" id="password" placeholder="Ingresa tu contraseña">
            </div>
            <button type="submit" class="btn btn-primary btn-lg btn-block">Iniciar Sesión</button>
            <div class="row justify-content-center mt-3">
                <button type="button" class="btn btn-danger btn-lg" @click="goBack">Regresar</button>
            </div>
        </form>
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