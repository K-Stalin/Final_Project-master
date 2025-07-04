<template>
  <v-app-bar app dense flat class="glass-navbar">
    <v-container class="d-flex justify-space-between align-center">
      <!-- Logo -->
      <v-img src="@/assets/Logo.svg" alt="logo" max-width="120" contain />

      <!-- Navigation Links -->
      <div class="d-flex align-center">
        <router-link
          v-for="(link, index) in navLinks"
          :key="index"
          :to="link.to"
          class="nav-link mx-3 font-weight-medium"
        >
          {{ link.text }}
        </router-link>

        <!-- Register Button -->
        <v-btn
          color="deep-purple accent-4"
          class="white--text ml-4"
          rounded
          elevation="2"
        >
          <v-icon left>mdi-account-plus</v-icon>
          Register Now
        </v-btn>
      </div>
    </v-container>
  </v-app-bar>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      navLinks: [
        { text: "Home", to: "/login" },
        { text: "About", to: "/login" },
        { text: "Contact", to: "/login" },
        { text: "Profile", to: "/login" },
        { text: "Settings", to: "/login" },
      ],
    };
  },
};
</script>

<style scoped>
.glass-navbar {
  background-color: rgba(255, 255, 255, 0.9) !important;
  backdrop-filter: blur(10px);
  border-bottom: 2px solid transparent;
  border-image: linear-gradient(to right, #8e2de2, #4a00e0) 1;
}

.nav-link {
  color: #333;
  text-decoration: none;
  position: relative;
  transition: 0.3s;
}

.nav-link::after {
  content: "";
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0%;
  height: 2px;
  background-color: #4a00e0;
  transition: width 0.3s ease-in-out;
}

.nav-link:hover::after {
  width: 100%;
}
</style>
