<template>
  <div id="app">
    <AppNavbar @view-change="changeView"></AppNavbar>
    <MainView v-if="currentView === 'main'" @view-change="changeView"></MainView>
    <LoginView v-if="currentView === 'login'" @view-change="changeView"></LoginView>
    <CustomerView v-if="currentView === 'customer'" @view-change="changeView"></CustomerView>
    <DriverView v-if="currentView === 'driver'" @view-change="changeView"></DriverView>
    <RideRequestView v-if="currentView === 'ride-request'" @view-change="changeView"></RideRequestView>
    <RideActiveView v-if="currentView === 'ride-active'" @view-change="changeView"></RideActiveView>
  </div>
</template>

<script>
import AppNavbar from './components/AppNavbar.vue';
import MainView from './components/MainView.vue';
import LoginView from './components/LoginView.vue';
import CustomerView from './components/CustomerView.vue';
import DriverView from './components/DriverView.vue';
import RideRequestView from './components/RideRequestView.vue';
import RideActiveView from './components/RideActiveView.vue';

export default {
  name: 'App',
  components: {
    AppNavbar,
    MainView,
    LoginView,
    CustomerView,
    DriverView,
    RideRequestView,
    RideActiveView
  },
  data() {
    return {
      currentView: 'login'
    };
  },
  methods: {
    changeView(view) {
      this.currentView = view;
    }
  }
};
</script>

<style>
@import 'https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css';
@import 'https://unpkg.com/leaflet/dist/leaflet.css';

body {
  background-color: #333;
  color: #fff;
}
</style>
