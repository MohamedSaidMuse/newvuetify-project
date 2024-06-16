<template>
    <div>
      <h1>Data Fetcher</h1>
      <div v-if="backendData">
        <h2>Backend Data:</h2>
        <pre>{{ backendData }}</pre>
      </div>
      <div v-else>
        <p>Loading data from the backend...</p>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'DataFetcher',
    data() {
      return {
        backendData: null,
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      async fetchData() {
        try {
          const response = await axios.get(process.env.VUE_APP_API_URL);
          this.backendData = response.data;
          console.log('Response from backend:', response.data); // Log the response data
        } catch (error) {
          console.error('There was an error fetching the data:', error);
          // Optionally, handle the error in the UI as well
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  </style>