<template>
  <div>
    Componente Chat Messages
    <div v-for="message in messages" :key="message.id">
      {{ message.message }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
      messages: []
  },
  data() {
    return {
    };
  },
  methods: {
    limpar() {
      this.messages = [];
    },
  },
};
</script>