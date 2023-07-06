import EmployeeList

<template>
  <div className="list-employee"><h1>Employee List</h1></div>
  <div>
    <employee-list></employee-list>
  </div>
</template>

<script>
import EmployeeList from "../src/components/EmployeeList.vue";

export default {
  components: {
    EmployeeList,
  },
};
</script>
