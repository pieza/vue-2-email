<template>
  <Messages :messages="outgoingMessages" />
</template>

<script>
import Messages from './Messages.vue'

export default {
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  computed: {
    outgoingMessages() {
      return this.data.messages.filter(
        message => message.type == 'outgoing' && !message.isDeleted
      )
    }
  },
  components: {
    Messages
  }
}
</script>
