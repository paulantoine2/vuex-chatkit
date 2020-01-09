<template>
  <div class="message-list">
    <h2># {{ activeRoom.name }}</h2>
    <hr>
    <div class="messages" v-chat-scroll="{smooth: true}">
      <div class="message"
           v-for="(message, index) in messages"
           :key="index"
           v-bind:class="{ 'current': message.username === user.username }">
        <div class="message__user">{{ message.username }}</div>
        <div class="message__text">{{ message.text }}</div>
        <div class="message__time">{{ message.date }}</div>
      </div>
    </div>
    <div class="typing" v-if="userTyping"><strong>{{ userTyping }}</strong> is typing...</div>
  </div>
</template>
<script>
import { mapState } from 'vuex'

export default {
  name: 'message-list',
  computed: {
    ...mapState([
      'messages',
      'activeRoom',
      'userTyping',
      'user'
    ])
  }
}
</script>
