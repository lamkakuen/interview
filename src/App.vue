<template>
  <div>
    <SearchModule></SearchModule>
    <Button></Button>
    <!-- Use other custom components here -->
  </div>
  <div>
    <TimeDisplay :timeZone="timeZone" :localTime="localTime" />
  </div>
  <TableWithPagination :records="records" />
  <div>
    <LocationButton @location-updated="handleLocationUpdated" />
    <MapDisplay :latitude="latitude" :longitude="longitude" />
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
        latitude: 42.7566742,
        longitude: -79.411775,
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
      console.log(this.latitude);
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
