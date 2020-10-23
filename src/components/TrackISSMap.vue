<template>
  <section>
    <div id="app">
      <mapbox
        access-token="your access token"
        :map-options="{
          style: 'mapbox://styles/mapbox/light-v9',
          center: [-96, 37.8],
          zoom: 3,
        }"
      />
    </div>
  </section>
</template>

<script>
import Mapbox from "mapbox-gl-vue";

export default {
  components: { Mapbox },
};
</script>

<style scoped>
#map {
  width: 100%;
  height: 500px;
}
</style>
</style>