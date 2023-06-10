<template>
    <button @click="getLocation">Get Location</button>
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