<template>
  <div class="message-form">
    <form @submit.prevent="onSubmit">
      <input id="message-input"
             type="text"
             placeholder="Enter a message"
             autocomplete="off"
             required
             @input="onTyping"
             v-model="message">
      <input type="submit" value="Send">
    </form>
  </div>
</template>
<script>
import { mapState, mapGetters, mapActions } from 'vuex'
import { isTyping } from '../chatkit'

export default {
  data () {
    return {
      message: ''
    }
  },
  methods: {
    ...mapActions([
      'sendMessage'
    ]),
    async onTyping () {
      await isTyping(this.activeRoom.id)
    },
    async onSubmit () {
      const res = await this.sendMessage(this.message)
      if (res) {
        this.message = ''
      }
    }
  },
  computed: {
    ...mapState([
      'user',
      'sending',
      'error',
      'activeRoom'
    ]),
    ...mapGetters([
      'hasError'
    ])
  }
}
</script>
