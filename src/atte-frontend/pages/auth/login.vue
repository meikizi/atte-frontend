<template>
  <div class="login">
    <AuthHeader></AuthHeader>
    <div class="login__container">
      <h1 class="login-title">ログイン</h1>
      <input v-model="email" class="email" type="email" name="email" placeholder="メールアドレス" />
      <input v-model="password" class="password" type="password" name="password" placeholder="パスワード" />
      <button @click="login" class="login-btn">ログイン</button>
      <div class="nav">
          <p class="nav-message">アカウントをお持ちでない方はこちらから</p>
          <NuxtLink to="/auth/register" class="nav-link">新規登録</NuxtLink>
      </div>
    </div>
    <AuthFooter></AuthFooter>
  </div>
</template>

<script>
  import '~/assets/css/login.css'

  export default {
      auth: false,
      data() {
          return {
              email: null,
              password: null
          }
      },
      methods: {
          async login() {
              try {
                  const response = await this.$auth
                      .loginWith("laravelSanctum", {
                          data: {
                              email: this.email,
                              password: this.password,
                          }
                      })
                      .then(() => {
                          // ログインに成功したら、/にページ遷移
                          window.alert("ログインしました");
                          this.$router.push("/");
                      });
                  console.log(response);
              } catch (error) {
                  // ログインに失敗したら、コンソールに出力する
                  window.alert("ログイン失敗");
                  console.log(error);
              }
          }
      }
  }
</script>
