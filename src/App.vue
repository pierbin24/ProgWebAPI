<template>
  <div id="app">
    <body>
      <header class="top-bar spread">
        <nav class="top-bar-nav">
          <router-link to="/" class="top-bar-link">Home</router-link> |
          <router-link to="/trips" class="top-bar-link">Trips</router-link>
          <button @click="toggleBox" class="button-add-trip">
            <span>Search Trip</span>
          </button>
          <button @click="toggleBox" class="button-add-trip">
            <span>Add Trip</span>
          </button>
        </nav>
        <router-link to="/trips" class="top-bar-login-link">Login</router-link>
      </header>
      <router-view />
      <AddTrip v-if="showbox" />
    </body>
  </div>
</template>

<script>
import trips from "./assets/trips.json";
import AddTrip from "./components/AddTrip.vue";

export default {
  name: "App",
  components: {
    AddTrip,
  },

  data() {
    return {
      trips: trips,
      showbox: false,
    };
  },
  methods: {
    toggleBox() {
      this.showbox = !this.showbox;
    },
  },
};
</script>

<style></style>
