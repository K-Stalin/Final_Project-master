<template>
  <v-container fluid class="pa-6 portfolio-wrapper">
    <!-- Header -->
    <h2 class="text-h5 font-weight-bold mb-6">📊 My Portfolio</h2>

    <!-- Summary -->
    <v-row dense class="mb-6">
      <v-col cols="12" md="4">
        <v-card class="summary-card pa-4">
          <h4 class="text-caption text--secondary">Total Investment</h4>
          <div class="text-h6 font-weight-bold">₹{{ totalInvestment }}</div>
        </v-card>
      </v-col>
      <v-col cols="12" md="4">
        <v-card class="summary-card pa-4">
          <h4 class="text-caption text--secondary">Current Value</h4>
          <div class="text-h6 font-weight-bold">₹{{ currentValue }}</div>
        </v-card>
      </v-col>
      <v-col cols="12" md="4">
        <v-card class="summary-card pa-4">
          <h4 class="text-caption text--secondary">Total P&L</h4>
          <div
            :class="totalPnL >= 0 ? 'green--text' : 'red--text'"
            class="text-h6 font-weight-bold"
          >
            ₹{{ totalPnL }}
          </div>
        </v-card>
      </v-col>
    </v-row>

    <!-- Portfolio Table -->
    <v-card class="pa-4">
      <v-simple-table dense>
        <thead>
          <tr>
            <th class="text-left">Stock</th>
            <th class="text-right">Qty</th>
            <th class="text-right">Buy Price</th>
            <th class="text-right">Current Price</th>
            <th class="text-right">Value</th>
            <th class="text-right">P&L</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="stock in holdings" :key="stock.name">
            <td class="text-left">{{ stock.name }}</td>
            <td class="text-right">{{ stock.qty }}</td>
            <td class="text-right">₹{{ stock.buyPrice }}</td>
            <td class="text-right">₹{{ stock.currentPrice }}</td>
            <td class="text-right">₹{{ stock.qty * stock.currentPrice }}</td>
            <td
              class="text-right"
              :class="
                (stock.currentPrice - stock.buyPrice) * stock.qty >= 0
                  ? 'green--text'
                  : 'red--text'
              "
            >
              ₹{{
                ((stock.currentPrice - stock.buyPrice) * stock.qty).toFixed(2)
              }}
            </td>
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
      holdings: [
        { name: "TCS", qty: 10, buyPrice: 3500, currentPrice: 3740 },
        { name: "HDFC Bank", qty: 5, buyPrice: 1550, currentPrice: 1610 },
        { name: "Wipro", qty: 20, buyPrice: 420, currentPrice: 400 },
      ],
    };
  },
  computed: {
    totalInvestment() {
      return this.holdings
        .reduce((sum, s) => sum + s.qty * s.buyPrice, 0)
        .toFixed(2);
    },
    currentValue() {
      return this.holdings
        .reduce((sum, s) => sum + s.qty * s.currentPrice, 0)
        .toFixed(2);
    },
    totalPnL() {
      return (this.currentValue - this.totalInvestment).toFixed(2);
    },
  },
};
</script>

<style scoped>
.portfolio-wrapper {
  background-color: #f9fafb;
  min-height: 100vh;
}

.summary-card {
  background-color: #ffffff;
  border-radius: 16px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.05);
}

.v-simple-table th,
.v-simple-table td {
  font-size: 14px;
}

.green--text {
  color: #2e7d32 !important;
}

.red--text {
  color: #c62828 !important;
}
</style>
