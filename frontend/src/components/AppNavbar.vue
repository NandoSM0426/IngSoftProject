<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <a class="navbar-brand" href="#">Uver</a>
        <button class="navbar-toggler" type="button" @click="toggleNavbar" aria-controls="navbarNav"
            aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" :class="{ show: isNavbarOpen }" id="navbarNav">
            <ul class="navbar-nav ml-auto">
                <li class="nav-item active">
                    <a class="nav-link" href="#" @click="showMainView">Inicio <span class="sr-only">(current)</span></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#" @click="showLoginView">Perfil</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Configuración</a>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script>
export default {
    name: 'AppNavbar',
    data() {
        return {
            isNavbarOpen: false
        };
    },
    methods: {
        toggleNavbar() {
            this.isNavbarOpen = !this.isNavbarOpen;
        },
        showMainView() {
            this.$emit('view-change', 'main');
        },
        showLoginView() {
            this.$emit('view-change', 'login');
        }
    }
};
</script>

<style scoped>
.navbar-dark .navbar-nav .nav-link {
    color: rgba(255, 255, 255, 0.75);
}

.navbar-dark .navbar-nav .nav-link:hover {
    color: white;
}
</style>