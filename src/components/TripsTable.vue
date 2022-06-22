<template>
  <div>
    <ChangeTrip v-if="showbox" />
    <p id="data" class="trip-table"></p>
  </div>
</template>

<script>
import ChangeTrip from "./ChangeTrip.vue";

export default {
  name: "TripsTable",
  components: {
    ChangeTrip,
  },
  props: ["tripsList", "toggle"],
  data() {
    return {
      showbox: true,
    };
  },
  methods: {
    toggleBox() {
      console.log("lessgo");
      this.showbox = !this.showbox;
    },
    async getTrips() {
      //let toogle= this.toggleBox();
      let trips = await this.tripsList;
      let disp = "";
      if (trips.length > 0) {
        disp = `
      <table class="trips-table">
      <tr>
      <th>Data</th>
      <th>Mezzo</th>
      <th>Coordinate</th>
      <th>Tappe</th>
      <th class="trips-modifier">Modify</th>
      </tr>
    `;
        //cosi posso mettere solo una tappa
        for (let i = 0; i < trips.length; i++) {
          disp +=
            '<tr class="trips-show-modifier"> <td>' + trips[i].data + "</td>";
          disp += "<td>" + trips[i].mezzo + "</td> ";
          disp +=
            "<td>" +
            "lat: " +
            trips[i].coordinate[0] +
            " lon: " +
            trips[i].coordinate[1] +
            "</br> lat: " +
            trips[i].coordinate[2] +
            " lon: " +
            trips[i].coordinate[3] +
            "</td> ";
          disp +=
            "<td>" +
            "lat: " +
            trips[i].tappe[0] +
            " lon: " +
            trips[i].tappe[1] +
            "</td> " +
            '<td class="trips-modifier"><button<button @click="toggleBox()" class="button-add-trip">' +
            "<span> Modifica </span>" +
            "</button></td> </tr>";
        }
        disp += "</table";
      } else {
        disp += "<h2>No trip yet</h2>";
        //aggiungo un pulsante aggiunfi viaggio
      }

      document.getElementById("data").innerHTML = disp;
    },
  },

  async mounted() {
    await this.getTrips();
  },
};
</script>
