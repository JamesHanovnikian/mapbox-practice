<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="doMapBox()"> Start Mapbox</button>
    <button v-on:click="locationLoop()"> Show Markers</button>
     
    
    <div id='map' style='width: 400px; height: 300px;'></div>
    </div> 
  </div>
</template>

<style></style>

<script>
import mapboxgl from "mapbox-gl";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      places: [
        { lat: 41.881832, lng: -87.623177, description: "Chicago!" },
        { lat: 37.9779, lng: 23.77, description: "Zografou!" },
        { lat: 37.787, lng: 20.8999, description: "zakynthos!" },
      ],
    };
  },
  mounted: function () {
    this.doMapBox();
  },
  created: function () {},
  methods: {
    doMapBox: function () {
      mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
      const map = new mapboxgl.Map({
        container: "map", // container ID
        style: "mapbox://styles/mapbox/cjaudgl840gn32rnrepcb9b9g", // style URL
        center: [-119.5591, 37.715], // starting position [lng, lat]
        zoom: 9, // starting zoom
      });
      map.on("load", function () {
        map.addSource("dem", {
          type: "raster-dem",
          url: "mapbox://mapbox.mapbox-terrain-dem-v1",
        });
        map.addLayer(
          {
            id: "hillshading",
            source: "dem",
            type: "hillshade",
          },
          "waterway-river-canal-shadow"
        );
      });
    },
  },
};
</script>

