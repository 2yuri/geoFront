<template>
  <div class="diveer">
    <l-map
      :zoom="zoom"
      :center="center"
      style="height: 200px; width: 100%"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
      <l-marker :lat-lng="marker" />
      <l-icon-default :image-path="path" />
    </l-map>
  </div>
</template>

<script>
import { latLng, Icon } from "leaflet";
import { LMap, LTileLayer, LMarker, LIconDefault } from "vue2-leaflet";


delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
  iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
  iconUrl: require('leaflet/dist/images/marker-icon.png'),
  shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
});


export default {
  
  name: "MapTES",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LIconDefault
  },
  data() {
    return {
      zoom: 13,
      path: "/images/",
      center: [47.41322, -1.219482],
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      marker: latLng(47.41322, -1.219482)
    };
  }
};
</script>

<style>
.diveer {
  width: 100%;
  height: 80%;
}
</style>