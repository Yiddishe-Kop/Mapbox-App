<template>
  <MglMap
    :accessToken="accessToken"
    :mapStyle="mapStyle"
    :center="center"
    :zoom="zoom"
    :pitch="pitch"
    :bearing="bearing"
    @click="getCoordinates"
    @load="onMapLoaded"
  >
    <MglNavigationControl position="top-right" />
    <MglGeolocateControl position="top-right" />
    <MglFullscreenControl position="top-right" />
    <MglScaleControl position="bottom-right" />
    <MglAttributionControl position="bottom-right" />

    <MglMarker
      v-for="marker in markers"
      :key="marker.coordinates[0]"
      class="map-marker"
      :coordinates="marker.coordinates"
      color="blue"
    >
      <Icon slot="marker" icon="torah">{{marker.name}}</Icon>
      <MglPopup :closeButton="false">
        <Card :title="marker.name">
          <p>
            Here is the holiest place on Earth.
            The Kosel Hamaaravi. הכותל
          </p>
        </Card>
      </MglPopup>
    </MglMarker>
  </MglMap>
</template>
<script>
import Mapbox from "mapbox-gl";
import {
  MglMap,
  MglAttributionControl,
  MglNavigationControl,
  MglGeolocateControl,
  MglFullscreenControl,
  MglScaleControl,
  MglMarker,
  MglPopup
} from "vue-mapbox";
import Icon from "@/components/UI/Icon";
import Card from "@/components/UI/Card";
import "@/assets/mapbox.scss";
import markers from "@/utils/markers";

export default {
  name: "home",
  components: {
    MglMap,
    MglAttributionControl,
    MglNavigationControl,
    MglGeolocateControl,
    MglFullscreenControl,
    MglScaleControl,
    MglMarker,
    MglPopup,
    Icon,
    Card
  },
  data() {
    return {
      accessToken:
        "pk.eyJ1IjoieWlkZGlzaGUta29wIiwiYSI6ImNrNXR2M24ybjA5ZmUzbG96ZnEzNTNsM3YifQ.YiOjCiSZKFunicAXXnQMHg",
      mapStyle: "mapbox://styles/mapbox/light-v10",
      center: [35.234307186140086, 31.776628302133233], // The Kosel
      zoom: 17,
      pitch: 45,
      bearing: 17,
      markers: markers
    };
  },
  methods: {
    getCoordinates(e) {
      console.log(e.mapboxEvent.lngLat.wrap());
    },
    onMapLoaded(event) {
      this.$store.map = event.map;
    }
  },
  created() {
    this.mapbox = Mapbox;
  }
};
</script>

<style lang="scss">
.mgl-map-wrapper {
  flex: 1;
  width: 100%;
  height: calc(100vh - 70px);
  .mapboxgl-map {
    height: calc(100vh - 70px);
  }
  svg.icon {
    height: 34px;
  }
}
</style>
