<template>
  <form @submit.prevent="submitForm" class="card shadow-sm p-3 mb-4 bg-light">
    
    <h5 class="mb-3 text-secondary">
      {{ localEmployee.id ? "Update Employee" : "Add Employee" }}
    </h5>

    <div class="row g-3">

      <div class="col-md-3">
        <input v-model="localEmployee.name" 
               class="form-control" 
               placeholder="Full Name" required />
      </div>

      <div class="col-md-2">
        <input v-model="localEmployee.designation" 
               class="form-control" 
               placeholder="Designation" required />
      </div>

      <div class="col-md-2">
        <input v-model="localEmployee.department" 
               class="form-control" 
               placeholder="Department" required />
      </div>

      <div class="col-md-2">
        <input v-model="localEmployee.salary" 
               type="number" 
               class="form-control" 
               placeholder="Salary" required />
      </div>

      <div class="col-md-3 d-grid">
        <button class="btn btn-success">
          {{ localEmployee.id ? "Update" : "Add" }}
        </button>
      </div>

    </div>
  </form>
</template>

<script>
export default {
  props: ["employee"],

  data() {
    return {
      localEmployee: this.employee
        ? { ...this.employee }
        : {
            id: null,
            name: "",
            designation: "",
            department: "",
            salary: ""
          }
    };
  },

  watch: {
    employee(newVal) {
      this.localEmployee = newVal
        ? { ...newVal }
        : {
            id: null,
            name: "",
            designation: "",
            department: "",
            salary: ""
          };
    }
  },

  methods: {
    submitForm() {
      this.$emit("save", this.localEmployee);
      this.resetForm();
    },

    resetForm() {
      this.localEmployee = {
        id: null,
        name: "",
        designation: "",
        department: "",
        salary: ""
      };
    }
  }
};
</script>