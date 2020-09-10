<template>
  <q-page class="row">
    <!-- <div class="div div--left">
      <div class="div--left--content shadow-21 column justify-center items-center">
      <img class="image--map" src="../assets/yuri.svg" alt="">
      <q-input class="q-mb-md full-width" label-color="primary" filled label="Rua"/>
      <q-input class="q-mb-md full-width" label-color="primary" filled label="Numero"/>
      <q-input class="q-mb-md full-width" label-color="primary" filled label="Cidade"/>
      <q-btn class="full-width q-pa-sm q-mt-sm" color="primary" label="Procurar"/>
      </div>
    </div> -->
    <map />
    
  </q-page>
</template>

<script>
  export default {
    components: {
      map: require('components/MapTES.vue').default
    }
  }
</script>

<style scoped>

.div {
  widows: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.div--left {
  background: #ccc;
}

.div--left--content {
  width: 78%;
  height: 90%;
  padding: 0 40px 40px 40px;
  border-radius: 10px;
  background: white;
}

.div--right {
  width: 100%;
  height: 100%;
}


.image--map {
  width: 50%;
}


</style>