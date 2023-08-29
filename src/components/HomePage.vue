<template>
  <form @submit="onSubmit">
    <div class="input-group mb-3">
      <span class="input-group-text" id="basic-addon1">id</span>
      <input
        required
        v-model="form.id"
        type="search"
        class="form-control"
        placeholder="Employee ID"
        aria-label="Username"
        aria-describedby="basic-addon1"
      />
    </div>
  </form>
  <EmployeePage :key="form.id" :id="form.id" />
</template>

<script>
import EmployeePage from "./EmployeePage.vue";

export default {
  components: { EmployeePage },
  name: "HomePage",
  data() {
    return {
      form: {
        id: "",
      },
    };
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
    },
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
