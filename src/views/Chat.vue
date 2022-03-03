<template>
  <v-card>
    <v-card-title>
      <chat-messages :messages="chat.messages" />
    </v-card-title>
    <v-card-text>
      <chat-form v-on:eventSendMessage="sendMessage" />
      <chat-users :users="chat.users" />
    </v-card-text>
  </v-card>
</template>

<script>
import ChatForm from "../components/ChatForm.vue";
import ChatMessages from "../components/ChatMessages.vue";
import ChatUsers from "../components/ChatUsers.vue";
export default {
  components: { ChatForm, ChatMessages, ChatUsers },
  data() {
    return {
      chat: {
        messages: [
          { id: 1, message: "Olá", userName: "Messi" },
          { id: 2, message: "Bom dia", userName: "Messi" },
        ],
        users: [
          {
            id: 1,
            name: "Isaque",
          },
          {
            id: 2,
            name: "João",
          },
          {
            id: 3,
            name: "Maria",
          },
        ],
      },
    };
  },
  methods: {
    sendMessage(message) {
      this.chat.messages.push({
        id: this.chat.messages.length + 1,
        message: message,
        userName: "Messi",
      });
    },
  },
};
</script>