<script>
import { useCounterStore } from '../stores/counter'
import { mapActions, mapWritableState } from 'pinia'
import NavBar from '../components/NavBar.vue'

export default {
  data() {
    return {
      registerForm: {
        username: '',
        email: '',
        password: '',
        phoneNumber: '',
        address: ''
      }
    }
  },
  components: { NavBar },
  computed: {
    ...mapWritableState(useCounterStore, ['isAuthenticated'])
  },
  methods: {
    ...mapActions(useCounterStore, ['register']),
    async submitRegister() {
      const res = await this.register(this.registerForm)

      this.$router.push({ name: 'login' })
    }
  }
}
</script>

<template>
  <div>
    <NavBar />
    <div class="register-page">
      <div class="register-form">
        <h2>Register</h2>
        <form @submit.prevent="submitRegister">
          <div class="form-group">
            <label for="username">Username:</label>
            <input type="text" id="username" v-model="registerForm.username" required />
          </div>
          <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" v-model="registerForm.email" required />
          </div>
          <div class="form-group">
            <label for="password">Password:</label>
            <input type="password" id="password" v-model="registerForm.password" required />
          </div>
          <div class="form-group">
            <label for="phoneNumber">PhoneNumber: </label>
            <input
              type="phoneNumber"
              id="phoneNumber"
              v-model="registerForm.phoneNumber"
              required
            />
          </div>
          <div class="form-group">
            <label for="address">address: </label>
            <input type="address" id="address" v-model="registerForm.address" required />
          </div>
          <button type="submit">Register</button>
        </form>
      </div>
    </div>
  </div>
</template>

<style>
.register-page {
  display: flex;
  justify-content: center; /* Center horizontally */
  align-items: center; /* Center vertically */
  height: 85vh; /* 100% viewport height */
}

.register-form {
  text-align: center; /* Center the content within the register-form div */
}

.form-group {
  margin-bottom: 1rem; /* Add margin between form groups */
}

/* Add other necessary styles for form elements */
</style>
