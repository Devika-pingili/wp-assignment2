<template>
  <div class="table-responsive">
    <table class="table table-hover table-bordered align-middle text-center shadow-sm">

      <thead class="table-primary">
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Designation</th>
          <th>Department</th>
          <th>Salary</th>
          <th>Actions</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="emp in employees" :key="emp.id">
          <td class="fw-bold">{{ emp.id }}</td>
          <td>{{ emp.name }}</td>
          <td>{{ emp.designation }}</td>
          <td>{{ emp.department }}</td>
          <td class="text-success fw-semibold">₹ {{ emp.salary }}</td>
          
          <td>
            <button 
              class="btn btn-outline-warning btn-sm me-2"
              @click="$emit('edit', emp)">
              Edit
            </button>

            <button 
              class="btn btn-outline-danger btn-sm"
              @click="$emit('delete', emp.id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>

    </table>
  </div>
</template>

<script>
export default {
  props: ["employees"]
};
</script>