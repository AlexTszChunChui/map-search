<template>
  <map-title />
  <map-view :searchHistory="searchHistory"></map-view>
  <map-search @submit-search="storedSearchHistory"></map-search>
  <time-zone v-if="searchHistory.length > 0" :searchHistory="searchHistory"></time-zone>
  <show-search-history @submit-delete="deleteHistory" :searchHistory="searchHistory"></show-search-history>
</template>

<script>
import MapTitle from './components/MapTitle.vue';
import MapView from './components/MapView.vue';
import MapSearch from './components/MapSearch.vue';
import ShowSearchHistory from './components/ShowSearchHistory.vue';
import TimeZone from './components/TimeZone.vue';

export default {
  components: {
    MapTitle,
    MapView,
    MapSearch,
    ShowSearchHistory,
    TimeZone,
  },
  data() {
    return {
      searchHistory: [{
        id: 1,
        searchParams: 'Zurich',
        coordinates: [16.62662018, 49.2125578],
        checked: false,
      }
      ]
    }
  },
  provide() {
    return {
      toggleDelete: this.toggleDelete
    }
  },
  methods: {
    storedSearchHistory(coordinates, searchParams) {
      this.searchHistory.unshift({
        id: new Date().toISOString(),
        coordinates,
        searchParams,
        checked: false,
      });
    },
    toggleDelete(id) {
      const target = this.searchHistory.find(((search) => search.id === id));
      target.checked = !target.checked;
    },
    deleteHistory() {
      this.searchHistory = this.searchHistory.filter(search => search.checked !== true);
    },
  }
}
</script>

<style></style>
