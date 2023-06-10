<template>
    <div class="time-display">
      <div class="time-zone">{{ timeZone }}</div>
      <div class="local-time">{{ localTime }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      timeZone: {
        type: String,
        required: true,
      },
      localTime: {
        type: String,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .time-display {
    text-align: center;
  }
  
  .time-zone {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 8px;
  }
  
  .local-time {
    font-size: 24px;
    font-weight: bold;
  }
  </style>