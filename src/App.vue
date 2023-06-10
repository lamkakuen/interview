<template>
  <div>
    <Button></Button>
    <!-- Use other custom components here -->
  </div>
  <div>
    <TimeDisplay :timeZone="timeZone" :localTime="localTime" />
  </div>
  <TableWithPagination :records="records" />
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
      // Implement the logic to handle the search term received from the SearchModule component
      // You can perform any necessary operations, such as updating the map or table with the search term

      // Example logic:
      // 1. Update the map with the new location
      // 2. Add a marker for the searched location
      // 3. Update the table with the new location

      // Example code:
      // Assuming you have a map instance available in the component's data

      // 1. Update the map with the new location
      const geocoder = new google.maps.Geocoder();
      geocoder.geocode({ address: searchTerm }, (results, status) => {
        if (status === 'OK') {
          const location = results[0].geometry.location;
          this.map.setCenter(location);
        } else {
          console.error('Geocode was not successful for the following reason: ' + status);
        }
      });

      // 2. Add a marker for the searched location
      const marker = new window.google.maps.Marker({
        position: this.map.getCenter(),
        map: this.map,
        title: searchTerm,
      });

      // 3. Update the table with the new location
      // Assuming you have a data property named 'locations' in the component to store the searched locations
      this.locations.push({
        name: searchTerm,
        // Include any other relevant information about the location
      });
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
