<template>
  <div class="container py-4">
    <div class="card shadow-lg">
      <div class="card-body">

        <h2 class="text-center text-primary mb-4">
          Employee Management System
        </h2>

        <EmployeeForm 
          :employee="selectedEmployee"
          @save="handleSave"
        />

        <EmployeeTable 
          :employees="employees"
          @edit="handleEdit"
          @delete="handleDelete"
        />

      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import EmployeeForm from "./components/EmployeeForm.vue";
import EmployeeTable from "./components/EmployeeTable.vue";

export default {
  components: { EmployeeForm, EmployeeTable },

  data() {
    return {
      api: "https://69e7501068208c1debe8a754.mockapi.io/api/employees",
      employees: [],
      selectedEmployee: null
    };
  },

  methods: {
    async fetchEmployees() {
      const res = await axios.get(this.api);
      this.employees = res.data;
    },

    async handleSave(emp) {
      if (emp.id) {
        await axios.put(`${this.api}/${emp.id}`, emp);
      } else {
        await axios.post(this.api, emp);
      }
      this.fetchEmployees();
      this.selectedEmployee = null;
    },

    handleEdit(emp) {
      this.selectedEmployee = emp;
    },

    async handleDelete(id) {
      await axios.delete(`${this.api}/${id}`);
      this.fetchEmployees();
    }
  },

  mounted() {
    this.fetchEmployees();
  }
};
</script>