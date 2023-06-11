<template>
 <div>
    <Button></Button>
    <!-- Use other custom components here -->
  </div>
  <div>
    <TimeDisplay :timeZone="timeZone" :localTime="localTime" />
  </div>
  <div>
    <TableWithPagination ref="tableRef" />
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
  computed: {
    paginatedRecords() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.records.value.slice(startIndex, endIndex);
    },
    // Rest of your computed properties...
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
        records: [],
        recordId: 0,
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
      this.records = [];
      this.latitude = searchTerm.latitude;
      this.longitude = searchTerm.longitude;
      
      //const locationData = searchTerm.address;
      //const latitudeData = this.latitude;
      //const longitudeData = this.longitude;
      this.recordId++;
      const newRecord = {
        id: this.recordId,
        location: searchTerm.address,
        latitude: searchTerm.latitude,
        longitude: searchTerm.longitude,
      };
      this.addRecord(newRecord);
      console.log(this.records);
      this.mapKey += 1;
    },
    deleteRecords(selectedIndices) {
      // Filter out the selected records from the locations array based on the selected record indices
      this.records = this.records.filter((record, index) => !selectedIndices.includes(index));
    },
    addRecord(record) {
      this.records.push(record);
      this.callTableMethod(record);
    },
    callTableMethod(record) {
      this.$refs.tableRef.addRecord(record); // Replace `methodName` with the actual method name in TableWithPagination
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
