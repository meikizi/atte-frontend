<template>
    <div class="auth-header">
      <div class="header__container">
        <nav class="link-area">
          <ul class="menu-group">
            <li class="menu-item">
              <NuxtLink to="/auth/register" class="link">新規登録</NuxtLink>
            </li>
            <li class="menu-item">
              <NuxtLink to="/auth/login" class="link">ログイン</NuxtLink>
            </li>
          </ul>
        </nav>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
    };
  },
};
</script>
