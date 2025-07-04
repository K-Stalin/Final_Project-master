<template class="overall">
  <v-container fluid class="stock-page-wrapper pa-6">
    <!-- Heading -->
    <h2 class="text-h5 font-weight-bold white--text">📊 Stocks</h2>
    <p class="text-caption grey--text mb-6">Browse and trade stocks from major exchanges.</p>

    <!-- Search Bar -->
    <v-card flat class="search-bar d-flex align-center px-4 py-2 mb-6">
      <v-icon left class="mr-2 grey--text">mdi-magnify</v-icon>
      <v-text-field
        v-model="search"
        hide-details
        solo
        flat
        dense
        placeholder="Search stocks by symbol or name..."
        class="flex-grow-1"
      ></v-text-field>
      <v-btn outlined small class="ml-2 white--text" color="blue darken-1">Filter</v-btn>
    </v-card>

    <!-- Stock List -->
    <h3 class="text-subtitle-1 font-weight-bold white--text mb-3">All Stocks</h3>

    <v-card
      v-for="(stock, index) in filteredStocks"
      :key="index"
      flat
      class="stock-item d-flex justify-space-between align-center pa-4 mb-3"
    >
      <!-- Left -->
      <div>
        <div class="d-flex align-center">
          <v-icon :color="stock.watchlist ? 'yellow' : 'grey'" small class="mr-2">
            {{ stock.watchlist ? 'mdi-star' : 'mdi-star-outline' }}
          </v-icon>
          <span class="white--text font-weight-bold mr-2">{{ stock.symbol }}</span>
          <v-chip x-small color="yellow darken-3" text-color="white" v-if="stock.watchlist">Watchlist</v-chip>
        </div>
        <div class="grey--text text-caption mt-1">{{ stock.name }}</div>
        <div class="grey--text text-caption">Vol: {{ stock.volume }} | Cap: {{ stock.cap }}</div>
      </div>

      <!-- Right -->
      <div class="text-right">
        <div class="font-weight-bold white--text text-h6">${{ stock.price }}</div>
        <div :class="stock.change >= 0 ? 'green--text' : 'red--text'" class="text-caption mb-2">
          {{ stock.change >= 0 ? '+' : '' }}{{ stock.change }} ({{ stock.changePercent }})
        </div>
        <div class="d-flex justify-end">
          <v-btn small color="green lighten-1" class="mr-2 white--text" @click="openDialog('buy', stock)">Buy</v-btn>
          <v-btn small color="red lighten-1" class="white--text" @click="openDialog('sell', stock)">Sell</v-btn>
        </div>
      </div>
    </v-card>

    <!-- BUY / SELL DIALOG -->
    <v-dialog v-model="dialog" max-width="400">
      <v-card>
        <v-card-title class="headline">{{ dialogType === 'buy' ? 'Buy' : 'Sell' }} {{ selectedStock?.symbol }}</v-card-title>
        <v-card-text>
          <v-text-field
            v-model.number="quantity"
            label="Enter Quantity"
            type="number"
            min="1"
            outlined
          />
          <div class="mt-2">
            <strong>Total:</strong>
            ₹{{ (quantity * (selectedStock?.price || 0)).toFixed(2) }}
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn text color="grey" @click="dialog = false">Cancel</v-btn>
          <v-btn color="primary" @click="confirmTransaction">
            Confirm {{ dialogType === 'buy' ? 'Buy' : 'Sell' }}
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      search: "",
      dialog: false,
      dialogType: "buy",
      selectedStock: null,
      quantity: 1,
      stocks: [
        {
          symbol: "AAPL",
          name: "Apple Inc.",
          price: 175.5,
          change: +2.34,
          changePercent: "+1.35%",
          volume: "45.2M",
          cap: "2.8T",
          watchlist: true,
        },
        {
          symbol: "TSLA",
          name: "Tesla Inc.",
          price: 245.3,
          change: -5.67,
          changePercent: "-2.26%",
          volume: "32.1M",
          cap: "775B",
          watchlist: true,
        },
        {
          symbol: "MSFT",
          name: "Microsoft Corp.",
          price: 332.1,
          change: +1.85,
          changePercent: "+0.56%",
          volume: "28.9M",
          cap: "2.5T",
          watchlist: false,
        },
        {
          symbol: "GOOGL",
          name: "Alphabet Inc.",
          price: 2650.0,
          change: +15.45,
          changePercent: "+0.59%",
          volume: "20.2M",
          cap: "1.6T",
          watchlist: false,
        },
      ],
    };
  },
  computed: {
    filteredStocks() {
      if (!this.search) return this.stocks;
      return this.stocks.filter((s) =>
        (s.symbol + s.name).toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
  methods: {
    openDialog(type, stock) {
      this.dialogType = type;
      this.selectedStock = stock;
      this.quantity = 1;
      this.dialog = true;
    },
    confirmTransaction() {
      alert(
        `${this.dialogType === "buy" ? "✅ Bought" : "🚫 Sold"} ${
          this.quantity
        } shares of ${this.selectedStock.symbol} for ₹${(
          this.quantity * this.selectedStock.price
        ).toFixed(2)}`
      );
      this.dialog = false;
    },
  },
};
</script>

<style scoped>
.stock-item {
  background-color: #1e293b;
  border-radius: 12px;
  transition: box-shadow 0.2s ease;
  box-shadow: 0 0 12px rgba(255, 255, 255, 0.06); /* soft white glow */
}

.stock-item:hover {
  box-shadow: 0 0 18px rgba(255, 255, 255, 0.1); /* a bit stronger on hover */
}

.search-bar {
  background-color: #1e293b;
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
}

.v-card-title,
.v-card-text,
.v-card-actions {
  background-color: #1e293b !important;
  color: #ffffff;
}

.v-dialog .v-card {
  background-color: #1e293b;
  color: white;
  border-radius: 12px;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.08);
}

.v-text-field input {
  color: white !important;
}

.v-text-field input::placeholder {
  color: #94a3b8 !important;
}

</style>
