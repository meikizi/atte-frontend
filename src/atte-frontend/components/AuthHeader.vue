<template>
    <div class="auth-header">
      <div class="header__container">
        <NuxtLink to="/" class="home">Atte</NuxtLink>
        <nav  v-if="this.$auth.loggedIn" class="link-area">
          <ul class="menu-group">
            <li class="menu-item">
              <NuxtLink to="/" class="link">ホーム</NuxtLink>
            </li>
            <li class="menu-item">
              <span v-if="this.$auth.loggedIn" class="logout-link" @click="logout">
                ログアウト
              </span>
            </li>
          </ul>
        </nav>
      </div>
    </div>
</template>

<script>
  import '~/assets/css/reset.css'
  import '~/assets/css/header.css'

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
