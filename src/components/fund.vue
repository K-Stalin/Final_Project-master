<template>
  <v-container fluid class="pa-8 fund-page">
    <!-- Page Title -->
    <h2 class="text-h5 font-weight-bold mb-6">💰 Funds</h2>

    <!-- Balance Summary -->
    <v-card flat class="pa-6 summary-card mb-6">
      <v-row align="center" justify="space-between">
        <div>
          <h3 class="text-subtitle-1 grey--text text--darken-2 mb-2">Available Balance</h3>
          <div class="text-h6 font-weight-bold">₹{{ balance.toLocaleString() }}</div>
        </div>
        <v-btn outlined color="primary" @click="refreshBalance">
          <v-icon left>mdi-refresh</v-icon> Refresh
        </v-btn>
      </v-row>
    </v-card>

    <!-- Fund Actions -->
    <v-row>
      <!-- Add Funds -->
      <v-col cols="12" md="6">
        <v-card outlined class="pa-6 action-card">
          <h3 class="text-subtitle-1 font-weight-medium mb-4">Add Funds</h3>
          <v-text-field
            v-model="amountToAdd"
            type="number"
            label="Enter Amount (₹)"
            outlined
            dense
            prepend-inner-icon="mdi-currency-inr"
          />
          <v-btn block color="primary" @click="addFunds">Add Funds</v-btn>
        </v-card>
      </v-col>

      <!-- Withdraw Funds -->
      <v-col cols="12" md="6">
        <v-card outlined class="pa-6 action-card">
          <h3 class="text-subtitle-1 font-weight-medium mb-4">Withdraw Funds</h3>
          <v-text-field
            v-model="amountToWithdraw"
            type="number"
            label="Enter Amount (₹)"
            outlined
            dense
            prepend-inner-icon="mdi-currency-inr"
          />
          <v-btn block color="error" @click="withdrawFunds">Withdraw Funds</v-btn>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      balance: 50000,
      amountToAdd: "",
      amountToWithdraw: "",
    };
  },
  methods: {
    refreshBalance() {
      alert("🔄 Balance refreshed");
    },
    addFunds() {
      if (this.amountToAdd) {
        this.balance += parseFloat(this.amountToAdd);
        alert(`✅ ₹${this.amountToAdd} added`);
        this.amountToAdd = "";
      }
    },
    withdrawFunds() {
      if (this.amountToWithdraw) {
        const amount = parseFloat(this.amountToWithdraw);
        if (amount > this.balance) {
          alert("❌ Insufficient funds");
        } else {
          this.balance -= amount;
          alert(`💸 ₹${this.amountToWithdraw} withdrawn`);
        }
        this.amountToWithdraw = "";
      }
    },
  },
};
</script>

<style scoped>
.fund-page {
  background-color: #f5f7fa;
  min-height: 100vh;
}

.summary-card {
  background-color: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
}

.action-card {
  background-color: #ffffff;
  border-radius: 12px;
  border: 1px solid #e0e0e0;
  transition: box-shadow 0.2s ease;
}

.action-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}
</style>
