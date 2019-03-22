<template>
  <div class="messenger-wrapper">
    <div class="messenger">
      <span class="chat-header">
        <span class="chat-title">
          Messenger
        </span>
      </span>
      <div id="chat" class="chat-window">
        <ul class="chat-container">
          <li
            v-for="(msg, idx) in this.messages"
            v-bind:key="idx"
            class="chat-item"
            v-bind:class="{ 'from-server': msg.remote }"
          >
            {{ msg.text }}
          </li>
        </ul>
      </div>
      <div class="message-input">
        <input type="text" v-model="message"  v-on:keyup.enter="handleMessage" :placeholder="this.greetings"/>
        <button @click="handleMessage" class="send-button">
          Send
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Chat',
  props: {
    greetings: String,
    messages: Array,
    sendMessage: Function,
  },
  data: function () {
      return {
          message: ""
      }
  },
  mounted() {

  },
  methods:  {
      handleMessage() {
        this.sendMessage(this.message)
        this.message = ""
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./styles.scss"></style>
