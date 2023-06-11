<template>
  <div class="container">
    <div class="header">
      <h1>Geoff Lam Location App</h1>
    </div>
    <div class="content">
      <div class="left-panel">
        <div class="time-display">
          <TimeDisplay :timeZone="timeZone" :localTime="localTime" />
        </div>
        <div class="map-display">
          <MapDisplay :key="mapKey" :latitude="latitude" :longitude="longitude" :ref="mapDisplayRef" />
        </div>
      </div>
      <div class="right-panel">
        <div class="search-location">
          <SearchModule @search-location="handleSearch" />
          <LocationButton @location-updated="handleLocationUpdated" />
        </div>
        <div class="table-with-pagination">
          <TableWithPagination ref="tableRef" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MapDisplay from './components/MapDisplay.vue';
import SearchModule from './components/SearchModule.vue';
import TableWithPagination from './components/TableWithPagination.vue';
import TimeDisplay from './components/TimeDisplay.vue';
import LocationButton from './components/LocationButton.vue';
export default {
  props: {
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
        timeZone: 'Eastern Daylight Time', // Variable to store the time zone
        localTime: '', // Variable to store the local time
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
      this.timeZone = searchTerm.timeZoneName;
      this.localTime = searchTerm.currentTime;
      console.log(searchTerm);
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
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.content {
  display: flex;
  justify-content: center;
  background-color: #f5f5f5;
}

.header {
    background-color: #96969665;
    padding: 20px;
  }

  .table-with-pagination{
    margin-top: 3px;
  }

</style>
