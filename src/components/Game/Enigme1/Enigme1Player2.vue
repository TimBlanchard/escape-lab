<template>
  <div class="screenContainer -enigme1">
    <PhoneCallIncoming v-if="isFakeCalling" :duration="isFakeCallingDuration" @onEndCall="endFakeCall" />
    <PhoneLocked
      v-else-if="!recalled || callEnd"
      :called="!recalled && isStart && !callEnd"
      :message="messageEnd"
      @onRecall="recall"
    />
    <PhoneCall v-else />
  </div>
</template>

<script>
import PhoneCall from './phoneBlocks/phoneCall.vue'
import PhoneCallIncoming from './phoneBlocks/phoneCallIncoming.vue'
import PhoneLocked from './phoneBlocks/phoneLocked.vue'

const SECOND_CALL = 15000

export default {
  name: 'Enigme1Player2',
  components: {
    PhoneCallIncoming,
    PhoneCall,
    PhoneLocked
  },
  data() {
    return {
      isFakeCalling: true,
      isFakeCallingDuration: 3500,
      isStart: false,
      recalled: false,
      messageEnd: {
        contact: '',
        message: ''
      },
      callEnd: false
    }
  },
  sockets: {
    startEnigme: function () {
      this.start()
      this.$data.isStart = true
    },
    'enigme1-end': function ({ messages }) {
      // console.log('enigme1-end', messages)
      this.$data.callEnd = true

      this.$data.messageEnd.contact = messages[0].contact
      this.$data.messageEnd.message = messages[0].messages[0].content
    },
    'enigme1-endNotRecall': function ({ contact, message }) {
      this.$data.messageEnd = { contact, message }
    },
    'enigme1-restart': function () {
      this.$data.isFakeCalling = true
      this.$data.isFakeCallingDuration = 3500
      this.$data.isStart = false
      this.$data.recalled = false
      this.$data.messageEnd = {
        contact: '',
        message: ''
      }
      this.$data.callEnd = false

      this.$socket.emit('readyTutoEnigme')

      // TODO : remove sounds
    }
  },
  mounted() {
    this.secondCall()
  },
  methods: {
    start() {
      console.log('START ENIGME')
    },
    endFakeCall() {
      this.$data.isFakeCalling = false
    },
    recall() {
      this.$data.recalled = true
      this.$socket.emit('enigme1-recall')
    },
    secondCall() {
      setTimeout(() => {
        if (this.$data.recalled) return

        this.$data.isFakeCallingDuration = 1000
        this.$data.isFakeCalling = true
      }, SECOND_CALL)
    }
  }
}
</script>
