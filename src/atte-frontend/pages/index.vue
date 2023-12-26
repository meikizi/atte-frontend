<template>
<div>
  <h1>ログインしました</h1>
  <p>{{ $auth.loggedIn }}</p>
  <p>{{ $auth.user }}</p>
  <p v-if="this.$auth.loggedIn" class="logout-link" @click="logout">
    <span class="text">ログアウト</span>
  </p>
</div>
</template>

<script>
export default {
  methods: {
    async logout() {
      try {
        await this.$auth.logout();
        location.reload();
      } catch (e) {}
    },
  },
}
</script>
