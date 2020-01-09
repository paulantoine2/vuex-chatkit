<template>
  <div class="login-form">
    <h4>Login Form</h4>
    <form @submit.prevent="onSubmit">
      <label for="username"></label>
      <input id="username"
              type="text"
              placeholder="Enter a username"
              :disabled="loading"
              autocomplete="off"
              required
              v-model="userId">
      <button type="submit" :disabled="isValid">
        Login
      </button>
    </form>
    <div class="error" v-if="hasError">{{ error }}</div>
    <div class="info" v-if="loading">Connecting . . .</div>
  </div>
</template>
<script>
import { mapState, mapGetters, mapActions } from 'vuex'

export default {
  name: 'login-form',
  data () {
    return {
      userId: ''
    }
  },
  computed: {
    isValid: function () {
      const result = this.userId.length < 3
      return result || this.loading
    },
    ...mapState([
      'loading',
      'error'
    ]),
    ...mapGetters([
      'hasError'
    ])
  },
  methods: {
    ...mapActions([
      'login'
    ]),
    async onSubmit () {
      const res = await this.login(this.userId)
      console.log(res)
      if (res) this.$router.push('chat')
    }
  }
}
</script>
