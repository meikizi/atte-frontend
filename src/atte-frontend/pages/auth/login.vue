<template>
  <div class="login">
    <AuthHeader></AuthHeader>
    <div class="login__container">
      <h1 class="login-title">ログイン</h1>
      <validation-observer ref="obs" v-slot="ObserverProps">
        <validation-provider v-slot="{ errors }" rules="required">
          <input v-model="email" class="email" type="email" name="email" placeholder="メールアドレス" />
          <div class="error">{{ errors[0] }}</div>
        </validation-provider>
        <validation-provider v-slot="{ errors }" rules="required">
          <input v-model="password" class="password" type="password" name="password" placeholder="パスワード" />
          <div class="error">{{ errors[0] }}</div>
        </validation-provider>
        <button @click="login" class="login-btn" :disabled="ObserverProps.invalid || !ObserverProps.validated">ログイン</button>
      </validation-observer>
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
