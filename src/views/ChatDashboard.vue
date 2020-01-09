<template>
  <div class="dashboard-chat">
    <h1>Chat - {{user.name}}</h1>
    <a class="logout" @click="onLogout">Logout</a>
    <RoomList />
    <MessageList />
    <MessageForm />
    <UserList />
  </div>
</template>

<script>
import { mapState, mapActions, mapMutations } from 'vuex'

import MessageForm from '../components/MessageForm'
import MessageList from '../components/MessageList'
import RoomList from '../components/RoomList'
import UserList from '../components/UserList'

export default {
  name: 'ChatDashboard',
  components: {
    MessageForm,
    MessageList,
    RoomList,
    UserList
  },
  computed: {
    ...mapState([
      'user',
      'reconnect'
    ])
  },
  methods: {
    ...mapActions([
      'logout',
      'login'
    ]),
    ...mapMutations([
      'setReconnect'
    ]),
    onLogout () {
      this.$router.push({ path: '/' })
      this.logout()
    },
    unload () {
      if (this.user.username) {
        this.setReconnect(true)
      }
    }
  },
  mounted () {
    window.addEventListener('beforeunload', this.unload)
    if (this.reconnect) {
      this.login(this.user.username)
    }
  }
}
</script>
