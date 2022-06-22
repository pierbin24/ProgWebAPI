<template>
  <div class="trips">
    <div class="wrapper">
      <!-- <AddTrip v-if="showbox" /> -->
      <h2>Trips</h2>
      <TripsTable v-if="loaded" :tripsList="trips" />
    </div>
  </div>
</template>

<script>
import TripsTable from "../components/TripsTable.vue";
// import Trips from "../assets/trips.json";

export default {
  name: "TripsView",
  components: {
    TripsTable,
  },
  data() {
    return {
      trips: [],
      loaded: false,
    };
  },
  methods: {
    async getTripsFile() {
      const response = await fetch("http://localhost:3000/trips", {
        method: "GET",
      });
      let res = await response.json();
      return res;
    },
    async getTrips() {
      let tripsFile = await this.getTripsFile();
      for (let i = 0; i < tripsFile.count; i++) {
        this.trips.push(tripsFile.trips[i]);
        this.loaded = true;
      }
    },
  },

  async created() {
    await this.getTripsFile();
    await this.getTrips();
  },
};
</script>
