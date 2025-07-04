<template>
  <v-container fluid class="pa-6 dashboard-page">
    <!-- Greeting -->
    <h2 class="text-h5 font-weight-bold mb-6">
      👋 Welcome to MyTrade Dashboard
    </h2>

    <!-- Summary Cards -->
    <v-row dense>
      <v-col cols="12" sm="4">
        <v-card class="pa-5 stat-card" outlined elevation="2">
          <v-icon size="28" color="indigo" class="mb-2">mdi-bank</v-icon>
          <h4 class="text-subtitle-1 text--secondary mb-1">Total Investment</h4>
          <div class="text-h6 font-weight-bold">₹1,20,000</div>
        </v-card>
      </v-col>
      <v-col cols="12" sm="4">
        <v-card class="pa-5 stat-card" outlined elevation="2">
          <v-icon size="28" color="blue" class="mb-2">mdi-chart-line</v-icon>
          <h4 class="text-subtitle-1 text--secondary mb-1">Current Value</h4>
          <div class="text-h6 font-weight-bold">₹1,42,800</div>
        </v-card>
      </v-col>
      <v-col cols="12" sm="4">
        <v-card class="pa-5 stat-card" outlined elevation="2">
          <v-icon size="28" color="green" class="mb-2">mdi-cash</v-icon>
          <h4 class="text-subtitle-1 text--secondary mb-1">Profit / Loss</h4>
          <div class="text-h6 font-weight-bold green--text">+₹22,800</div>
        </v-card>
      </v-col>
    </v-row>

    <!-- Recent Activity -->
    <v-card class="pa-6 mt-6" outlined>
      <h3 class="text-subtitle-1 font-weight-medium mb-4">
        📌 Recent Activity
      </h3>
      <v-simple-table dense>
        <thead>
          <tr>
            <th>Date</th>
            <th>Action</th>
            <th>Stock</th>
            <th>Amount</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(txn, i) in recentTransactions" :key="i">
            <td>{{ txn.date }}</td>
            <td>{{ txn.type }}</td>
            <td>{{ txn.stock }}</td>
            <td>₹{{ txn.amount }}</td>
          </tr>
        </tbody>
      </v-simple-table>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      recentTransactions: [
        { date: "2025-07-03", type: "Buy", stock: "TCS", amount: 15000 },
        { date: "2025-07-02", type: "Sell", stock: "Infosys", amount: 8000 },
        { date: "2025-07-01", type: "Add Funds", stock: "-", amount: 20000 },
      ],
    };
  },
};
</script>

<style scoped>
.dashboard-page {
  background-color: #f9fafb;
  min-height: 100vh;
}

.stat-card {
  border-radius: 16px;
  transition: box-shadow 0.3s;
}

.stat-card:hover {
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}
</style>
