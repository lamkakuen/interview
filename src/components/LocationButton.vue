<template>
    <button class="button color-button" @click="getLocation">Get Current Location</button>
  </template>
  
  <script>
  export default {
    methods: {
      getLocation() {
        if (navigator.geolocation) {
          navigator.geolocation.getCurrentPosition(
            (position) => this.handlePosition(position),
            (error) => this.handleError(error)
          );
        } else {
          alert('Geolocation is not supported by this browser.');
        }
      },
      handlePosition(position) {
        const latitude = position.coords.latitude;
        const longitude = position.coords.longitude;

        // Emit the custom event with the latitude and longitude
        this.$emit('location-updated',  latitude, longitude );
        
        // Now you can use the latitude and longitude values as needed
        console.log('Latitude:', latitude);
        console.log('Longitude:', longitude);
        
      },
      handleError(error) {
        // Handle any errors that occur during geolocation
        console.error(error.message);
      },
    },
  };
  </script>

<style>
  .container {
    text-align: center;
  }

  .content {
    display: flex;
    /* Other styles for the content area */
  }
  .left-panel {
    display: flex;
    flex-direction: column;
    /* Other styles for the left panel */
  }

  .search-location {
    display: flex;
    align-items: center;
    /* Other styles for the search location section */
  }

  .right-panel {
    display: flex;
    flex-direction: column;
  }

  .color-button {
    background-color: #ff7f50;
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

  .button:hover {
    box-shadow: 0 2px 8px rgba(50, 50, 50, 0.3);
  }

  .button:active {
    box-shadow: 0 2px 8px rgba(50, 50, 50, 0.3);
  }
  /* Add additional styling as needed for other sections */
</style>