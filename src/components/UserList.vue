<template>
  <div class="user-list">
    <h2>User list</h2>
    <hr>
    <div class="user" v-for="user in users" :key="user.username">
      {{ user.name }}
      <div class="status" v-bind:class="user.presence"></div>
    </div>
  </div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  name: 'UserList',
  computed: {
    ...mapState([
      'loading',
      'users'
    ])
  }
}
</script>
