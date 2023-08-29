<template>
  <div class="card">
    <h2>
      <br />
      {{ name }} <br /><br />
    </h2>
  </div>
  <TicketRequests :id="id" />
</template>

<script>
import EmployeeService from "@/services/EmployeeService";
import TicketRequests from "./TicketRequests.vue";

export default {
  components: {
    TicketRequests,
  },
  name: "EmployeePage",
  props: {
    id: String,
  },
  data() {
    return {
      employeeID: String,
      name: "Name:",
      email: String,
      department: String,
      isAdmin: Boolean,
    };
  },
  created() {
    this.employeeID = this.id;

    EmployeeService.getAllEmployees().forEach((e) => {
      if (e.employee_id == this.id) {
        this.name = e.name;
        this.email = e.email;
        this.department = e.department;
        this.isAdmin = e.isAdmin == "yes" ? true : false;
      }
    });
  },
};
</script>

<style>
/* Card style credit to bootstrap */

.card {
  width: 254px;
  height: 254px;
  background: #07182e;
  position: relative;
  display: flex;
  place-content: center;
  place-items: center;
  overflow: hidden;
  border-radius: 20px;
}

.card h2 {
  z-index: 1;
  color: white;
  font-size: 2em;
  flex-wrap: wrap;
}

.card::before {
  content: "";
  position: absolute;
  width: 100px;
  background-image: linear-gradient(
    180deg,
    rgb(0, 183, 255),
    rgb(255, 48, 255)
  );
  height: 130%;
  animation: rotBGimg 3s linear infinite;
  transition: all 0.2s linear;
}

@keyframes rotBGimg {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

.card::after {
  content: "";
  position: absolute;
  background: #06244a;
  inset: 5px;
  border-radius: 15px;
}
/* .card:hover:before {
  background-image: linear-gradient(180deg, rgb(81, 255, 0), purple);
  animation: rotBGimg 3.5s linear infinite;
} */
</style>
