<template>
    <div>
      <table class="table">
        <thead>
          <tr>
            <th>
              <input type="checkbox" v-model="selectAll" @change="selectAllRecords" />
            </th>
            <th>Location</th>
            <th>Latitude</th>
            <th>Longitude</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="record in paginatedRecords" :key="record.id">
            <td>
              <input type="checkbox" v-model="selectedRecords" :value="record.id" />
            </td>
            <td>{{ record.location }}</td>
            <td>{{ record.latitude }}</td>
            <td>{{ record.longitude }}</td>
          </tr>
        </tbody>
      </table>
      <button @click="deleteSelectedRecords" class="button">Delete Selected</button>
      <div class="pagination">
        <button @click="previousPage" :disabled="currentPage === 1" class="button">Previous</button>
        <span>{{ currentPage }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages" class="button">Next</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        records: [], // Array to store searched places
        selectedRecords: [], // Array to store selected record IDs
        currentPage: 1, // Current page number
        pageSize: 10, // Number of records per page
        selectAll: false, // Flag to select all records
      };
    },
    name: 'CustomTableWithPagination',
    computed: {
      paginatedRecords() {
        const startIndex = (this.currentPage - 1) * this.pageSize;
        const endIndex = startIndex + this.pageSize;
        return this.records.slice(startIndex, endIndex);
      },
      totalPages() {
        return Math.ceil(this.records.length / this.pageSize);
      },
    },
    methods: {
      selectAllRecords() {
        if (this.selectAll) {
          this.selectedRecords = this.records.map((record) => record.id);
        } else {
          this.selectedRecords = [];
        }
      },
      deleteSelectedRecords() {
        // Code to delete selected records
      },
      previousPage() {
        if (this.currentPage > 1) {
          this.currentPage--;
        }
      },
      nextPage() {
        if (this.currentPage < this.totalPages) {
          this.currentPage++;
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .table {
    width: 100%;
    border-collapse: collapse;
  }
  
  .table th,
  .table td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  
  .pagination {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .pagination button {
    margin: 0 5px;
  }
  </style>