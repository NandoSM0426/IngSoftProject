<template>
    <div class="container mt-5">
        <h1 class="text-center text-white">Bienvenido a Uver</h1>
        <p class="text-center text-white">Elige cómo deseas usar la aplicación.</p>
        <div class="choice-container">
            <div class="choice-card">
                <h2>Cliente</h2>
                <p>Solicita un viaje y disfruta de nuestro servicio de transporte.</p>
                <button class="btn btn-primary btn-lg" @click="showCustomerView">Soy Cliente</button>
            </div>
            <div class="choice-card">
                <h2>Conductor</h2>
                <p>Regístrate como conductor y empieza a ganar dinero.</p>
                <button class="btn btn-secondary btn-lg" @click="showDriverView">Soy Conductor</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        showCustomerView() {
            this.$emit('view-change', 'customer');
        },
        showDriverView() {
            this.$emit('view-change', 'driver');
        }
    }
};
</script>

<style scoped>
body {
    background-color: #333;
    color: #fff;
}

.choice-container {
    display: flex;
    justify-content: space-around;
    margin-top: 50px;
}

.choice-card {
    background-color: #444;
    border: 1px solid #555;
    border-radius: 10px;
    padding: 20px;
    width: 300px;
    text-align: center;
}

.btn-primary {
    background-color: #555;
    border-color: #555;
}

.btn-primary:hover {
    background-color: #777;
    border-color: #777;
}

.btn-secondary {
    background-color: #777;
    border-color: #777;
}

.btn-secondary:hover {
    background-color: #999;
    border-color: #999;
}
</style>