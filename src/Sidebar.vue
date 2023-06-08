<template>
  <aside class="sm-side">
    <div class="user-head">
      <img src="https://avatars.githubusercontent.com/u/19609958?v=4" width="60" height="60">

      <div class="user-name">
        <h5>Jose Ulloa</h5>
        <span class="email-address">jandres258@hotmail.com</span>
      </div>
    </div>

    <div class="compose-wrapper">
      <Compose />
    </div>

    <ul class="inbox-nav">
      <li :class="{ active: activeView == 'Inbox' }">
        <a href="#" @click.prevent="navigate('Inbox', 'Inbox')">
          <i class="fa fa-inbox"></i>Inbox <span class="label label-danger pull-right">{{ unreadMessages.length }}</span>
        </a>
      </li>

      <li :class="{ active: activeView == 'Sent' }">
        <a href="#" @click.prevent="navigate('Sent', 'Sent')">
          <i class="fa fa-envelope-o"></i>Sent <span class="label label-default pull-right">{{ sentMessages.length
          }}</span>
        </a>
      </li>

      <li :class="{ active: activeView == 'Important' }">
        <a href="#" @click.prevent="navigate('Important', 'Important')">
          <i class="fa fa-bookmark-o"></i>Important <span class="label label-warning pull-right">{{
            importantMessages.length }}</span>
        </a>
      </li>

      <li :class="{ active: activeView == 'Trash' }">
        <a href="#" @click.prevent="navigate('Trash', 'Trash')">
          <i class="fa fa-trash-o"></i>Trash <span class="label label-default pull-right">{{ trashMessages.length
          }}</span>
        </a>
      </li>
    </ul>
  </aside>
</template>

<script>
import Compose from './Compose.vue'
import { eventBus } from './main'

export default {
  props: {
    messages: {
      type: Array,
      required: true
    }
  },
  created() {
    eventBus.$on('changeView', data => {
      this.activeView = data.tag
    })
  },
  data() {
    return {
      activeView: 'Inbox'
    }
  },
  methods: {
    navigate(newView, title) {
      eventBus.$emit('changeView', {
        tag: newView,
        title
      })
    }
  },
  computed: {
    unreadMessages() {
      return this.messages.filter(
        message => message.type == 'incoming' && !message.isRead && !message.isDeleted
      )
    },
    sentMessages() {
      return this.messages.filter(
        message => message.type == 'outgoing' && !message.isDeleted
      )
    },
    importantMessages() {
      return this.messages.filter(
        message => message.type == 'incoming' && message.isImportant && !message.isDeleted
      )
    },
    trashMessages() {
      return this.messages.filter(
        message => message.isDeleted
      )
    }
  },
  components: {
    Compose
  }
}
</script>
