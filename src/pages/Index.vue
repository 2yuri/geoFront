<template>
  <q-page class="row fullscreen">
    <div class="div div--left">
      <img src="./assets/map-dar;jpg1" alt="">
      <div class="div--left--content column justify-center">
      <q-input class="q-mb-md" filled label="Rua"/>
      <q-input class="q-mb-md" filled label="Numero"/>
      <q-input class="q-mb-md" filled label="Cidade"/>
      <q-btn class="full-width q-pa-xs" color="primary" label="Procurar"/>
      </div>
    </div>
    <div class="div div--right">
      <p class="text-white">mapa aq</p>
    </div>
    
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex'
}
</script>

<style scoped>

.div {
  height: 100vh;
  width: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.div--left {
  background: #ccc;
}

.div--left--content {
  width: 600px;
  height: 600px;
  padding: 40px;
  border-radius: 10px;
  background: white;
}

.div--right {
  background: blue;
}


</style>