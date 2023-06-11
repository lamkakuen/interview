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
            //const timeZone = results[0].timeZoneId;
            const apiKey = 'AIzaSyCkV5-OTH4mE87kMCAE-Hgm6wol_LvtZeM';
            const apiUrl = `https://maps.googleapis.com/maps/api/timezone/json?location=${latitude},${longitude}&timestamp=${Math.floor(Date.now() / 1000)}&key=${apiKey}`;
            
            fetch(apiUrl)
              .then(response => response.json())
              .then(data => {
                if (data.status === 'OK') {
                  const timeZoneId = data.timeZoneId;
                  const timeZoneName = data.timeZoneName;
                  
                  const currentTime = new Date().toLocaleString('en-US', {
                    timeZone: timeZoneId,
                    hour: 'numeric',
                    minute: 'numeric',
                    second: 'numeric'
                  });
                  this.$emit('search-location', {
                    address: this.searchTerm,
                    latitude,
                    longitude,
                    timeZoneName,
                    currentTime
                  });
                  // Use the time zone information as needed
                } else {
                  console.error('Unable to retrieve time zone information');
                }
              })
              .catch(error => {
                console.error('Error occurred while fetching time zone information:', error);
              });
              // Emit an event to notify the parent component about the searched location
            
            //console.log(location,latitude,longitude);
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