<template>
  <Messages :messages="trashMessages" />
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
    trashMessages() {
      return this.data.messages.filter(
        message => message.isDeleted
      )
    }
  },
  components: {
    Messages
  }
}
</script>
