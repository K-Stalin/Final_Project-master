<template>
  <v-container class="login_detail pa-8" elevation="2">
    <h2 class="mb-6 text-h5 font-weight-bold text-center">Get Started Now</h2>

    <v-form>
      <v-text-field
        v-model="form.name"
        label="Name"
        type="text"
        required
        outlined
        prepend-inner-icon="mdi-account-circle"
      />
      <v-text-field
        v-model="form.email"
        label="Email"
        type="email"
        required
        outlined
        prepend-inner-icon="mdi-email"
      />
      <v-text-field
        v-model="form.password"
        label="Password"
        type="password"
        required
        outlined
        prepend-inner-icon="mdi-lock"
      />
      <v-text-field
        v-model="form.confirmPassword"
        label="Confirm Password"
        type="password"
        required
        outlined
        prepend-inner-icon="mdi-lock"
      />

      <v-btn
        color="green darken-1"
        class="white--text mt-4"
        block
        large
        @click="submitForm"
      >
        Submit
      </v-btn>
    </v-form>
  </v-container>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      form: {
        name: "",
        email: "",
        password: "",
        confirmPassword: "",
      },
    };
  },
  methods: {
    submitForm() {
      // TODO: Add form validation / submission logic
      console.log("Form submitted:", this.form);
    },
  },
};
</script>

<style scoped>
.login_detail {
  max-width: 400px;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 100vh;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

@media screen and (max-width: 760px) {
  .login_detail {
    width: 90%;
    padding: 16px;
  }
}
</style>
