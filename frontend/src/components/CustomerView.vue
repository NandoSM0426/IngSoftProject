<template>
    <div class="container mt-5">
        <h1 class="text-center text-white">Bienvenido Cliente</h1>
        <p class="text-center text-white">Elige tu destino y disfruta del viaje.</p>
        <div id="map" style="height: 300px;"></div>
        <div class="form-group">
            <label for="destination">Destino:</label>
            <input type="text" class="form-control" id="destination" placeholder="Ingresa tu destino"
                @input="updateRoute">
        </div>
        <div class="form-group">
            <label for="payment-method">Método de Pago:</label>
            <select class="form-control" id="payment-method">
                <option>Tarjeta de Crédito</option>
                <option>PayPal</option>
                <option>Efectivo</option>
            </select>
        </div>
        <div class="row justify-content-center">
            <button class="btn btn-primary btn-lg mr-3" @click="requestRide">Solicitar Viaje</button>
            <button class="btn btn-secondary btn-lg" @click="showHistory">Ver Historial</button>
        </div>
        <div class="row justify-content-center mt-3">
            <button class="btn btn-danger btn-lg" @click="goBack">Regresar</button>
        </div>
    </div>
</template>

<script>
import L from 'leaflet';
import 'leaflet-routing-machine';

export default {
    data() {
        return {
            map: null,
            routeControl: null
        };
    },
    mounted() {
        this.initializeMap();
    },
    methods: {
        initializeMap() {
            this.map = L.map('map').setView([0, 0], 13);
            L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                maxZoom: 18,
            }).addTo(this.map);
            this.map.locate({ setView: true, maxZoom: 16 });
            this.map.on('locationfound', this.onLocationFound);
            this.map.on('locationerror', this.onLocationError);
        },
        onLocationFound(e) {
            var radius = e.accuracy / 2;
            L.marker(e.latlng).addTo(this.map)
                .bindPopup("Estás dentro de " + radius + " metros desde este punto").openPopup();
        },
        onLocationError(e) {
            alert(e.message);
        },
        requestRide() {
            this.$emit('view-change', 'ride-request');
            setTimeout(() => {
                this.$emit('view-change', 'ride-active');
            }, 3000);
        },
        goBack() {
            this.$emit('view-change', 'main');
        },
        updateRoute() {
            var destination = document.getElementById('destination').value;
            fetch('https://nominatim.openstreetmap.org/search?format=json&q=' + destination)
                .then(response => response.json())
                .then(data => {
                    if (data.length > 0) {
                        var destinationLocation = [data[0].lat, data[0].lon];
                        if (this.routeControl) {
                            this.map.removeControl(this.routeControl);
                        }
                        this.routeControl = L.Routing.control({
                            waypoints: [
                                L.latLng(this.map.getCenter()),
                                L.latLng(destinationLocation)
                            ],
                            lineOptions: {
                                styles: [{ color: '#3388ff', opacity: 1, weight: 5 }]
                            },
                            createMarker: function () { return null; }
                        }).addTo(this.map);
                    } else {
                        console.error('No se pudo encontrar el destino.');
                    }
                })
                .catch(error => console.error('Error al buscar el destino:', error));
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