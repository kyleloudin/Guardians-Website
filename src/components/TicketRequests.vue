<template>
  <div>
    <table class="table table-dark table-striped-columns">
      <thead>
        <tr>
          <th scope="col">Request ID</th>
          <th scope="col">Employee ID</th>
          <th scope="col">Number of Tickets Requested</th>
          <th scope="col">Day of Game</th>
          <th scope="col">Time of Entry</th>
          <th scope="col">Approval</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="request in requests" :key="request.employee_id">
          <th scope="row">{{ request.request_id }}</th>
          <td>{{ request.employee_id }}</td>
          <td>{{ request.number_of_tickets }}</td>
          <td>{{ request.game_date }}</td>
          <td>{{ request.entry_time }}</td>
          <td>{{ request.isApproved }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import TicketRequestService from "@/services/TicketRequestService";

export default {
  name: "TicketRequests",
  props: {
    id: String,
  },
  data() {
    return {
      requests: [],
      request: {
        request_id: String,
        employee_id: String,
        number_of_tickets: String,
        date_requested: String,
        game_date: String,
        entry_time: String,
        isApproved: String,
      },
    };
  },
  created() {
    this.employee_id = this.id;

    TicketRequestService.getAllTicketRequests().forEach((request) => {
      if (request.employee_id == this.id) {
        this.request.request_id = request.request_id;
        this.request.number_of_tickets = request.number_of_tickets;
        this.request.date_requested = request.date_requested;
        this.request.game_date = request.game_date;
        this.request.entry_time = request.entry_time;
        this.request.game_date = request.isApproved == "yes" ? true : false;
        this.requests.push(request);
      }
    });
  },
};
</script>

<style>
table-dark table-striped-columns {
  max-width: 90%;
}
</style>
