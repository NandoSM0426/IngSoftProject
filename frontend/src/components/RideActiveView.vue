<template>
    <div class="container mt-5">
        <h1 class="text-center text-white">Viaje en Progreso</h1>
        <p class="text-center text-white">Tu viaje está en curso. Disfruta del recorrido.</p>
        <div id="map-active" style="height: 300px;"></div>
        <div class="row justify-content-center mt-3">
            <button class="btn btn-danger btn-lg" @click="endRide">Finalizar Viaje</button>
        </div>
    </div>
</template>

<script>
import L from 'leaflet';
import 'leaflet-routing-machine';

export default {
    data() {
        return {
            mapActive: null
        };
    },
    mounted() {
        this.initializeMap();
    },
    methods: {
        initializeMap() {
            navigator.geolocation.getCurrentPosition(position => {
                var currentLocation = [position.coords.latitude, position.coords.longitude];
                this.mapActive = L.map('map-active').setView(currentLocation, 13);
                L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                    maxZoom: 18,
                }).addTo(this.mapActive);
                L.marker(currentLocation).addTo(this.mapActive)
                    .bindPopup('Inicio del viaje')
                    .openPopup();
                this.updateRoute(currentLocation);
            });
        },
        updateRoute(currentLocation) {
            var destination = document.getElementById('destination').value;
            fetch('https://nominatim.openstreetmap.org/search?format=json&q=' + destination)
                .then(response => response.json())
                .then(data => {
                    if (data.length > 0) {
                        var destinationLocation = [data[0].lat, data[0].lon];
                        L.Routing.control({
                            waypoints: [
                                L.latLng(currentLocation),
                                L.latLng(destinationLocation)
                            ],
                            lineOptions: {
                                styles: [{ color: '#3388ff', opacity: 1, weight: 5 }]
                            },
                            createMarker: function () { return null; }
                        }).addTo(this.mapActive);
                    } else {
                        console.error('No se pudo encontrar el destino.');
                    }
                })
                .catch(error => console.error('Error al buscar el destino:', error));
        },
        endRide() {
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