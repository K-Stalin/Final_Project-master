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
          <h4 class="text-subtitle-1 text--secondary mb-1">NIFTY 50</h4>
          <div class="text-h6 font-weight-bold">26,461.00</div>
        </v-card>
      </v-col>
      <v-col cols="12" sm="4">
        <v-card class="pa-5 stat-card" outlined elevation="2">
          <h4 class="text-subtitle-1 text--secondary mb-1">SENSEX</h4>
          <div class="text-h6 font-weight-bold">83,432.89</div>
        </v-card>
      </v-col>
      <v-col cols="12" sm="4">
        <v-card class="pa-5 stat-card" outlined elevation="2">
          <h4 class="text-subtitle-1 text--secondary mb-1">BANK NIFTY</h4>
          <div class="text-h6 font-weight-bold">57,031.00</div>
        </v-card>
      </v-col>
    </v-row>
    <v-container fluid class="pa-6">
    <h2 class="text-h5 font-weight-bold  mb-6">📈 Stock Overview</h2>

    <v-row dense>
      <v-col
        v-for="(stock, index) in stocks"
        :key="index"
        cols="12"
        sm="6"
        md="4"
        lg="3"
        xl="2"
      >
        <v-card class="pa-4 stock-card" flat>
          <div class="text-subtitle-1 font-weight-bold white--text">{{ stock.name }}</div>
          <div class="white--text mt-1">₹{{ stock.price }}</div>
          <div :class="stock.change >= 0 ? 'green--text' : 'red--text'" class="mt-1 text-caption">
            {{ stock.change >= 0 ? '+' : '' }}{{ stock.change }}
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>

  </v-container>
</template>

<script>
export default {
  data() {
    return {
      stocks: [
        { name: "Canara Bank", price: 2632.50, change: +184.90 },
        { name: "SBI", price: 615.3, change: -21.13 },
        { name: "HDFC Bank", price: 1520.4, change: +10.63 },
        { name: "ICICI Bank", price: 890.0, change: -34.53 },
        { name: "Axis Bank", price: 790.9, change: +59.11 },
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

.stock-card {
  background-color: #1e293b;
  border-radius: 12px;
  box-shadow: 0 0 12px rgba(255, 255, 255, 0.05);
  transition: 0.2s ease;
}
.stock-card:hover {
  box-shadow: 0 0 16px rgba(255, 255, 255, 0.1);
}
</style>
