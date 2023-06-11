<template>
 <div>
    <Button></Button>
    <!-- Use other custom components here -->
  </div>
  <div>
    <TimeDisplay :timeZone="timeZone" :localTime="localTime" />
  </div>
  <div>
    <TableWithPagination :records="records" />
  </div>
  <div>
    <LocationButton @location-updated="handleLocationUpdated" />
    <SearchModule @search-location="handleSearch"></SearchModule>
    <MapDisplay :key="mapKey" :latitude="latitude" :longitude="longitude" :ref="mapDisplayRef" />
  </div>
</template>

<script>

import MapDisplay from './components/MapDisplay.vue';
import SearchModule from './components/SearchModule.vue';
import TableWithPagination from './components/TableWithPagination.vue';
import TimeDisplay from './components/TimeDisplay.vue';
import Button from './components/Button.vue';
import LocationButton from './components/LocationButton.vue';
export default {
  props: {
    timeZone: String,
    localTime: String,
  },
  name: 'App',
  components: {
    Button,
    MapDisplay,
    SearchModule,
    TableWithPagination,
    TimeDisplay,
    LocationButton,
  },
  data() {
    return {
        latitude: 42,
        longitude: 42,
        mapKey: 1,
    };
  },
  methods: {
    //handleLocationAcquired(locationData) {
    //  this.latitude = locationData.latitude;
    //  this.longitude = locationData.longitude;
    //},
    handleLocationUpdated(latitude, longitude) {
      this.latitude = latitude;
      this.longitude = longitude;
      this.mapKey += 1;
    },
    handleSearch(searchTerm) {
      this.latitude = searchTerm.latitude;
      this.longitude = searchTerm.longitude;
      this.mapKey += 1;
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
