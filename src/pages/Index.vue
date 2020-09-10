<template>
  <q-page class="row fullscreen">
    <q-btn v-if="counter && $q.platform.is.mobile" @click="counter = false" class="button--add fixed-bottom-right" size="20px" round color="primary" icon="add" />
    <div v-if="!counter || $q.platform.is.desktop" :class="$q.platform.is.desktop ? 'div--left' : 'div--left--mobile'">
      <div class="div--left--content shadow-5 column justify-center items-center">
      <img @click="() => { this.zoom = 18 }" class="image--map q-mb-md" src="../assets/map.svg" alt="">
      <form class="full-width">
        <q-input
          v-model="street"
          type="text"
          class="q-mb-md full-width"
          filled
          autofocus
          label="Rua" 
        />
        <q-input
          v-model="number"
          type="text"
          class="q-mb-md full-width"
          filled
          label="Numero"
        />
        <q-input
          v-model="city"
          type="text"
          class="q-mb-md full-width"
          filled
          label="Cidade" 
        />
        <q-btn 
          :disable="this.city === '' || this.street === '' || this.number === ''"
          type="submit"
          @click="sendValue"
          class="full-width q-pa-sm q-mt-xs"
          color="primary"
          label="Procurar" 
        />
        </form>
      </div>
    </div>
    <div class="div div--right">
      <div class="div--right--content">
        <l-map
      :zoom="zoom"
      :center="center"
      style="height: 100%; width: 100%; border-radius: 10px;"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
      <l-marker :lat-lng="marker" />
      <l-icon-default :image-path="path" />
    </l-map>
      </div>
    </div>
    
  </q-page>
</template>

<script>
import { latLng, Icon } from "leaflet";
import axios from 'axios';
import { LMap, LTileLayer, LMarker, LIconDefault } from "vue2-leaflet";
import "leaflet/dist/leaflet.css"

delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
  iconRetinaUrl: require('assets/flag2x.png'),
  iconUrl: require('assets/flag.png'),
  shadowUrl: require('assets/shadow.png'),
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
      street: '',
      counter: false,
      number: '',
      city: '',
      lat: -24.9582553,
      long: -53.4197443,
      zoom: 3,
      currentZoom: 13,
      path: "/images/",
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    }
  },
  computed: {
    center: function () {
      return [this.lat, this.long]
    },
    marker: function () {
      return latLng(this.lat, this.long)
    }
  },
  created: 
    function () {
      this.sendValueFirstTime()
    }
  ,
  methods: {
    async sendValueFirstTime() {
      const { data } = await axios.post('http://192.168.0.22:3008/address', {
        street: 'Rua matelandia',
        number: '674',
        city: 'Cascavel',
        province: 'PR',
        country: 'Brasil'   
      })

      this.lat = data.infos.geoInformation.lat;
      this.long = data.infos.geoInformation.lng
      this.zoom = 16
    },
    async sendValue() {
      const { data } = await axios.post('http://192.168.0.22:3008/address', {
        street: this.street,
        number: this.number,
        city: this.city,
        province: '',
        country: ''   
      })

      this.lat = data.infos.geoInformation.lat;
      this.long = data.infos.geoInformation.lng
      this.zoom = 16

      this.street = null
      this.number = null
      this.city = null

      this.counter = true
    },
  }
};
</script>

<style scoped>

.div {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.div--left {
  background: transparent;
  top: calc(50% - 210px);
  left: 50px;
  position: absolute;
  z-index: 999;
}

.div--left--mobile {
  background: transparent;
  top: calc(50% - 210px);
  left: calc(50% - 150px);
  position: absolute;
  z-index: 999;
}

.div--left--content {
  width: 300px;
  height: 420px;
  padding: 0 20px 10px 20px;
  border-radius: 10px;
  background: white;
}

.button--add {
  z-index: 999;
  margin: 0px 10px 10px 0px;
}

.div--right {
background: #fff;
}

.div--right--content {
  width: 100vw;
  height: 100vh;
  border-radius: 10px;
}


.image--map {
  width: 30%;
}


</style>