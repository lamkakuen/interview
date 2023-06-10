<template>
    <button class="my-button" @click="handleClick">{{ buttonText }}</button>
  </template>
  
  <script>
  export default {
    data() {
      return {
        buttonText: 'Click Me',
      };
    },
    name: 'CustomButton',
    methods: {
      handleClick() {
        alert('Button clicked!');
      },
    },
  };
  </script>
  
  <style>
  .my-button {
    background-color: #007bff;
    color: #fff;
    padding: 8px 16px;
    font-size: 16px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .my-button:hover {
    background-color: #0056b3;
  }
  </style>