<template>
  <div>
      Usuários online:
    <div v-for="user in users" :key="user.id">
      {{ user }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    users: [],
  },
};
</script>