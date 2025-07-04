<template>
  <v-container>
    <h2 class="text-h5 font-weight-bold mb-4">Transaction History</h2>
    <v-data-table :headers="headers" :items="transactions" dense></v-data-table>
  </v-container>
</template>

<script>
export default {
  name: "Transactions",
  data() {
    return {
      headers: [
        { text: "Type", value: "type" },
        { text: "Stock", value: "stock" },
        { text: "Amount", value: "amount" },
        { text: "Date", value: "date" },
      ],
      transactions: [
        { type: "Buy", stock: "TCS", amount: "₹5000", date: "2025-07-03" },
        { type: "Sell", stock: "Infosys", amount: "₹3000", date: "2025-07-02" },
        { type: "Add Fund", stock: "-", amount: "₹10,000", date: "2025-07-01" },
      ],
    };
  },
};
</script>
