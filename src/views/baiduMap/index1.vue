<template>
  <div class="map-contaioner">
    <Map></Map>
  </div>
</template>

<script>
import Map from "./map1.vue";
export default {
  components: {
    Map,
  },
};
</script>

<style lang="scss">
.map-contaioner {
  height: 100%;
  width: 100%;
  position: relative;
}
</style>