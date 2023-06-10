<template>
    <div>
      <input v-model="searchTerm" type="text" placeholder="Enter location">
      <button @click="search">Search</button>
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
      search() {
        this.$emit('search-location', this.searchTerm);
        console.log(this.searchTerm);
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