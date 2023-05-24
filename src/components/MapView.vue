<template>
    <mgl-map mapStyle="https://api.maptiler.com/maps/streets/style.json?key=PS2Z0oN8xndXP36dLDUH" 
      :zoom="zoomLevel"
      :center="mapCenter">
      <mgl-marker 
      v-for="search in searchHistory" 
      :coordinates="search.coordinates" 
      :key="search.id" 
      color="#42b883"></mgl-marker>
      <mgl-navigation-control position="top-left" />
    </mgl-map>
</template>

<script>
import { MglMap, MglNavigationControl, MglMarker } from 'vue-maplibre-gl';

export default {
  props:['searchHistory'],
  computed: {
    mapCenter() {
      if (this.searchHistory.length < 1) {
        return [16.62662018, 49.2125578];
      } 
      return this.searchHistory[0].coordinates;
    },
    zoomLevel() {
      if (this.searchHistory.length <= 1) {
        return 3;
      } return 9;
    }
  },
  components: {
    MglMap,
    MglNavigationControl,
    MglMarker
  }
}
</script>

<sytle lang="scss" scoped>
@import "~vue-maplibre-gl/src/css/maplibre.scss";

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New', monospace;
}

#app {
  width: 100%;
  height: 40vh;
}
</sytle>