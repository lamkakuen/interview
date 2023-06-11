<template>
    <div>
      <div id="map"></div>
    </div>
  </template>
  
  <script>
  
  export default {
    data() {
      return {
        map: null,
      };
    },
    name: 'MapDisplay',
    mounted() {
      this.initMap();
    },
    props: {
        latitude: {
            type: Number,
            default: 0
        },
        longitude: {
            type: Number,
            default: 0
        }
    },
    methods: {
      initMap() {
        
        const map = new google.maps.Map(document.getElementById('map'), {
          center: { lat: this.latitude, lng: this.longitude },
          zoom: 8,
        });
  
        const marker = new google.maps.Marker({
          position: { lat: this.latitude, lng: this.longitude },
          map: map,
        });

        this.marker = marker;
      },
      initializeMap() {
        const mapOptions = {
          center: { lat: this.latitude, lng: this.longitude },
          zoom: 12,
        };
        this.map = new google.maps.Map(this.$refs.mapContainer, mapOptions);
      },
      updateMap() {
        if (this.map) {
            const newCenter = new google.maps.LatLng(this.latitude, this.longitude);
            this.map.setCenter(newCenter);
            
            // Remove the previous marker
            if (this.marker) {
            this.marker.setMap(null);
            }
            // Add a new marker
            this.marker = new google.maps.Marker({
            position: newCenter,
            map: this.map
            });
            }
        }
    },
    watch: {
        latitude: {
            immediate: true,
            handler() {
                this.updateMap();
            }
        },
            longitude: {
            immediate: true,
            handler() {
                this.updateMap();
            }
        }
    }
  };
  </script>
  
  <style>
  #map {
    height: 400px;
    width: 600px;
  }
  </style>