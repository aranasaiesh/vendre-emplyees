<template>
  <div class="employee-list">
    <div class="employee" v-for="employee in employees" :key="employee.id">
      <img :src="employee.avatar" class="profile-picture" />
      <div class="employee-details">
        <div class="employee-name">
          {{ employee.first_name }} {{ employee.last_name }}
        </div>
        <a :href="'mailto:' + employee.email" class="contact-link">Contact</a>
      </div>
    </div>

    <div class="pagination">
      <button @click="previousPage" :disabled="page === 1">Previous</button>
      <span>{{ page }}</span>
      <button @click="nextPage" :disabled="page === totalPages">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      employees: [],
      page: 1,
      totalPages: 0,
    };
  },
  mounted() {
    this.fetchEmployees();
  },
  methods: {
    fetchEmployees() {
      fetch(`https://reqres.in/api/users?page=${this.page}`)
        .then((response) => response.json())
        .then((data) => {
          this.employees = data.data;
          this.totalPages = data.total_pages;
        })
        .catch((error) => {
          console.error("Error fetching employees:", error);
        });
    },
    previousPage() {
      if (this.page > 1) {
        this.page--;
        this.fetchEmployees();
      }
    },
    nextPage() {
      if (this.page < this.totalPages) {
        this.page++;
        this.fetchEmployees();
      }
    },
  },
};
</script>

<style>
.employee-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.employee {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 30%;
  margin-bottom: 20px;
}

.profile-picture {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-bottom: 10px;
}

.employee-details {
  text-align: center;
}

.employee-name {
  font-weight: bold;
  color: darkslategray;
}

.contact-link {
  color: darkslategrey;
}

.contact-link:hover {
  color: rgb(162, 162, 162);
  text-decoration: underline;
}

.pagination {
  margin-top: 20px;
  text-align: center;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  background-color: rgba(255, 255, 255, 0.075);
  z-index: 1;
}

.pagination button {
  margin: 0 18px;
  background-color: #fee32b;
  color: black;
}

@media (max-width: 768px) {
  .employee {
    width: 48%;
  }
}
</style>
