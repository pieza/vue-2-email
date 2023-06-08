<template>
  <div class="container">
    <div class="mail-box">
      <Sidebar :messages="messages" />
      <Content :messages="messages" />
    </div>
  </div>
</template>

<script>
import Sidebar from './Sidebar.vue'
import Content from './Content.vue'
import messages from './data/messages'
import randomMessages from './data/random-messages'
import { eventBus } from './main'

export default {
  name: 'app',
  data() {
    return {
      messages
    }
  },
  created() {
    eventBus.$on('refreshMessages', () => {
      const randomIndex = Math.floor(Math.random() * randomMessages.length)
      const temp = [randomMessages[randomIndex]]
      this.messages = temp.concat(this.messages.slice(0))
    })
    eventBus.$on('sentMessage', (data) => {
      const temp = [data.message]
      this.messages = temp.concat(this.messages.slice(0))
    })
  },
  components: {
    Sidebar,
    Content
  }
}
</script>
