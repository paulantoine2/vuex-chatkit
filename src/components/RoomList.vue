<template>
  <div class="room-list">
    <h2>Rooms</h2>
    <hr>
    <div class="room"
         v-for="room in rooms"
         :key="room.id"
         v-bind:class="{ 'active': room.id === activeRoom.id }"
         @click="onRoomSelection(room.id)"
         >
      <span>#</span> {{ room.name }}
    </div>
  </div>
</template>
<script>
import { mapState, mapActions } from 'vuex'

export default {
  name: 'RoomList',
  computed: {
    ...mapState([
      'rooms',
      'activeRoom'
    ])
  },
  methods: {
    ...mapActions([
      'selectRoom'
    ]),
    onRoomSelection (roomId) {
      this.selectRoom(roomId)
    }
  }
}
</script>
