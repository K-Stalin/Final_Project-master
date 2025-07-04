<template>
  <v-app>
    <!-- Navigation Drawer (Sidebar) -->
    <v-navigation-drawer app clipped permanent width="240" color="#111827">
      <v-list nav dense>
        <!-- Brand -->
        <v-list-item class="py-5">
          <v-list-item-content>
            <v-list-item-title class="white--text text-h6 font-weight-bold">
              📈 MyTrade
            </v-list-item-title>
            <v-list-item-subtitle class="grey--text"
              >Grow Your Wealth</v-list-item-subtitle
            >
          </v-list-item-content>
        </v-list-item>

        <v-divider class="grey darken-3" />

        <!-- Navigation Items -->
        <v-list-item
          v-for="(item, i) in menuItems"
          :key="i"
          :value="item.component"
          @click="activePage = item.component"
          :class="[
            'nav-item',
            activePage === item.component ? 'nav-active' : '',
          ]"
          link
        >
          <v-list-item-icon>
            <v-icon class="white--text">{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title class="white--text">{{
              item.title
            }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- Main Content -->
    <v-main class="grey lighten-5">
      <component :is="activePageComponent" />
    </v-main>
  </v-app>
</template>

<script>
import Stocks from "../components/stocks.vue";
import Funds from "../components/fund.vue";
import Portfolio from "../components/portfolio.vue";
import Dashboard from "../components/dashboard.vue";
import Transactions from "../components/transactions.vue";

export default {
  components: {
    Stocks,
    Funds,
    Portfolio,
    Dashboard,
    Transactions,
  },
  data() {
    return {
      activePage: "Dashboard",
      menuItems: [
        {
          title: "Dashboard",
          icon: "mdi-view-dashboard",
          component: "Dashboard",
        },
        { title: "Stocks", icon: "mdi-finance", component: "Stocks" },
        { title: "Portfolio", icon: "mdi-briefcase", component: "Portfolio" },
        { title: "Funds", icon: "mdi-cash", component: "Funds" },
        {
          title: "Transactions",
          icon: "mdi-history",
          component: "Transactions",
        },
      ],
    };
  },
  computed: {
    activePageComponent() {
      return this.activePage;
    },
  },
};
</script>

<style scoped>
.v-navigation-drawer {
  border-right: 1px solid #1f2937;
}

.nav-item {
  transition: background 0.2s;
}

.nav-item:hover {
  background-color: #1e293b !important;
  border-left: 4px solid #4caf50;
}

.nav-active {
  background-color: #1e293b !important;
  border-left: 4px solid #4caf50;
}
</style>
