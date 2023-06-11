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
    <button  @click="deleteSelectedRecords" class="button d-color-button button:hover button:active">Delete Selected</button>
    <div class="pagination">
      <button @click="previousPage" :disabled="currentPage === 1" class="button">Previous</button>
      <span>{{ currentPage }}</span>
      <button @click="nextPage" :disabled="currentPage === totalPages || totalPages === 0" class="button">Next</button>
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
      // Filter out the selected records and update the records array
      this.records = this.records.filter((record) => {
        return !this.selectedRecords.includes(record.id);
      });

      // Clear the selectedRecords array
      this.selectedRecords = [];
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
    addRecord(record) {
      this.records.push(record);
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
  border: none;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    cursor: pointer;
    margin-left: 10px;
}
  .container {
  }

  .content {
    display: flex;
  }

  .left-panel {
    display: flex;
    flex-direction: column;
  }

  .search-location {
    display: flex;
    align-items: center;
  }

  .d-color-button {
    background-color: #ad1a2d;
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

  .p-color-button {
    background-color: #28b91b;
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

</style>
