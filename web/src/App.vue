<template>
  <div id="app">
    <Chat
      greetings="..."
      :messages="this.messages"
      :send-message="handleSendMessage"
    />
  </div>
</template>

<script>
import Chat from "./components/Chat.vue";

const api = async (url, msg) => {
  const myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/x-www-form-urlencoded");
  const bodyParams = new URLSearchParams();
  bodyParams.append("q", msg);
  const response = await fetch("/api/get-answer", {
    method: "post",
    headers: myHeaders,
    body: bodyParams
  });
  return response.json();
};

export default {
  name: "app",
  components: {
    Chat
  },
  data: function() {
    return {
      messages: [
        {
          remote: true,
          text: "Где деньги, Лебовски?"
        }
      ]
    };
  },
  methods: {
    async handleSendMessage(msg) {
      this.messages.push({ remote: false, text: msg });
      const resp = await api("/api/get-answer", msg);
      if (resp.ok) {
        this.messages.push({ remote: true, text: resp.a });
      } else {
        console.log("ERR:", resp.error);
      }
    }
  }
};
</script>