<template>
    <div>
      <input v-model="searchTerm" @keyup.enter="searchLocation" type="text" placeholder="Enter location">
      <button @click="searchLocation">Search</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchTerm: '', // Stores the search term entered by the user
      };
    },
    methods: {
      searchLocation() {
      // Call the geocode function to convert the search term into coordinates
        const geocoder = new google.maps.Geocoder();
        geocoder.geocode({ address: this.searchTerm }, (results, status) => {
          if (status === 'OK' && results.length > 0) {
            // Get the latitude and longitude from the first result
            const location = results[0].geometry.location;
            const latitude = location.lat();
            const longitude = location.lng();

            // Emit an event to notify the parent component about the searched location
            this.$emit('search-location', {
              address: this.searchTerm,
              latitude,
              longitude,
            });
            console.log(location,latitude,longitude);
          } else {
            console.error('Geocode was not successful for the following reason: ' + status);
          }
        });
      },
    },
  };
  </script>
  
  <style scoped>
  .input {
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }
  
  .button {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    cursor: pointer;
    margin-left: 10px;
  }
  </style>