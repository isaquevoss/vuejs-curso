<template>
  <v-container>
    <v-text-field prepend-icon="mdi-message" v-model="message">
      <v-btn slot="append" color="primary" @click="sendMessage"> Enviar </v-btn>
    </v-text-field>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      message: "",
    };
  },
  methods: {
    sendMessage() {
      this.$emit("eventSendMessage", this.message);
      this.message = "";
    },
  },
};
</script>