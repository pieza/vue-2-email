<template>
  <Messages :messages="importantMessages" />
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
    importantMessages() {
      return this.data.messages.filter(
        message => message.type == 'incoming' && message.isImportant && !message.isDeleted
      )
    }
  },
  components: {
    Messages
  }
}
</script>
