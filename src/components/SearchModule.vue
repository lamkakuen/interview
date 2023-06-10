<template>
    <div>
      <input type="text" v-model="location" @keyup.enter="searchLocation" class="input" placeholder="Enter a location" />
      <button @click="searchLocation" class="button">Search</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        location: '',
      };
    },
    name: 'CustomSearchModule',
    methods: {
      searchLocation() {
        // Code to search for the location
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