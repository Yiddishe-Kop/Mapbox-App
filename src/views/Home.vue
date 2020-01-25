<template>
  <div class="home">
    <div class="coordinates">{{coordinates}}</div>
    <Sidebar />
    <Map @mapdata="e => coordinates = e.coordinates" />
  </div>
</template>

<script>
import Sidebar from "@/components/Sidebar";
import Map from "@/components/Map";

export default {
  name: "home",
  components: { Map, Sidebar },
  data() {
    return {
      coordinates: undefined
    };
  },
  methods: {},
  mounted() {
    console.log({ Map });
  }
};
</script>

<style lang="scss">
.home {
  flex: 1;
  display: flex;

  .coordinates {
    position: absolute;
    z-index: 999;
  }
}
</style>
