<template>
  <div>
    <link
      rel="stylesheet"
      href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"
    />
    <l-map style="height: 300px" :zoom="zoom" :center="center">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>

      <l-marker
        v-for="marker in markers"
        :key="marker.id"
        :lat-lng.sync="marker.position"
      >
        <l-popup>
          <div>{{ popup[0] }}</div>
        </l-popup></l-marker
      >
      <!-- <l-marker
        v-for="marker in markers"
        :key="marker.id"
        :draggable="marker.draggable"
        :lat-lng.sync="marker.position"
      ></l-marker> -->
      <!-- <l-polyline
        :lat-lngs="polyline.latlngs"
        :color="polyline.color"
      ></l-polyline> -->
      <l-polyline
        v-for="item in polylines"
        :key="item.id"
        :lat-lngs="item.points"
        :visible="item.visible"
      />
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer, LPolyline, LMarker, LPopup } from "vue2-leaflet";

export default {
  props: ["tripsList"],
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPolyline,
    LPopup,
    //LTooltip
  },

  data() {
    return {
      zoom: 10,
      center: [51.505, -0.09],
      markers: [],
      polylines: [],
      popup: [],
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    };
  },

  methods: {
    async showTrip() {
      let trips = await this.tripsList;
      for (let i = 0; i < trips.length; i++) {
        this.popup.push(this.addPopup(trips[i]));
        let line = [];
        let point = [];
        for (let j = 0; j < 3; j++) {
          point[0] = trips[i].coordinate[j];
          point[1] = trips[i].coordinate[j + 1];
          this.addMarker(trips[i].coordinate[j], trips[i].coordinate[j + 1]);
          j++;
          line.push(point);
          point = [""]; //non so perchè se non lo pulisco dopo me li cambia entrambi
        }
        //posso farlo più bello ho messo due perchè il cilco avanza di due,
        //potrei fare un altra variable j che si incrementa solo di 1
        this.addPolyline(line[0], line[1]);
        line = [""];
      }
    },

    //   async showTrip() {
    //   let trips = await this.tripsList;
    //   console.log("trips: " + trips[0].data);
    //   this.popup.push(this.addPopup(trips[0]));
    //   let line = [];
    //   let point = [];
    //   for (let i = 0; i < 3; i++) {
    //     point[0] = trips[0].coordinate[i];
    //     point[1] = trips[0].coordinate[i + 1];
    //     this.addMarker(trips[0].coordinate[i], trips[0].coordinate[i + 1]);
    //     i++;
    //     line.push(point);
    //     point = [""]; //non so perchè se non lo pulisco dopo me li cambia entrambi
    //   }
    //   //posso farlo più bello ho messo due perchè il cilco avanza di due,
    //   //potrei fare un altra variable j che si incrementa solo di 1
    //   this.addPolyline(line[0], line[1]);
    // },

    addMarker(latitude, longitude) {
      const newMarker = {
        position: { lat: latitude, lng: longitude },
        visible: true,
      };
      this.markers.push(newMarker);
    },

    addPolyline(start, end) {
      const newPolyline = {
        points: [
          { lat: start[0], lng: start[1] },
          { lat: end[0], lng: end[1] },
        ],
        draggable: true,
        visible: true,
      };
      this.polylines.push(newPolyline);
    },

    removeMarker: function (index) {
      this.markers.splice(index, 1);
    },

    async addPopup(trips) {
      let popup = "";
      popup += "Data: " + trips.data;
      popup += " Mezzo: " + trips.mezzo;
      return popup;
    },
  },
  async mounted() {
    await this.showTrip();
  },
};
</script>

<!-- 
  show trip con i console log test
sync showTrip() {
      let tripsFile = await this.tripsFile;
      this.popup.push(await this.addPopup(tripsFile));
      console.log("Trip" + tripsFile.trips[0].coordinate);
      let line = [];
      let point = [];
      for (let i = 0; i < 3; i++) {
        console.log("x" + tripsFile.trips[0].coordinate[i]);
        point[0] = tripsFile.trips[0].coordinate[i];
        console.log("y" + tripsFile.trips[0].coordinate[i + 1]);
        point[1] = tripsFile.trips[0].coordinate[i + 1];
        console.log("point " + point);

        this.addMarker(
          tripsFile.trips[0].coordinate[i],
          tripsFile.trips[0].coordinate[i + 1]
        );
        i++;
        line.push(point);
        console.log("line " + line);
        point = [""]; //non so perchè se non lo pulisco dopo me li cambia entrambi
      }
      //posso farlo più bello ho messo due perchè il cilco avanza di due,
      //potrei fare un altra variable j che si incrementa solo di 1
      this.addPolyline(line[0], line[1]);
    }, -->
