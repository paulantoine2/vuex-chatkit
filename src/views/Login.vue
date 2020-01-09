<template>
  <div class="login">
    <h1>Vue Chat</h1>
    <h2>Powered by Vue and Pusher Chatkit - Made by Paul.ntn</h2>
    <LoginForm />
  </div>
</template>
<script>
import LoginForm from '@/components/LoginForm.vue'

export default {
  name: 'login',
  components: {
    LoginForm
  }
}
</script>
