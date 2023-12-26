<template>
  <div class="register">
    <AuthHeader></AuthHeader>
    <div class="register__container">
      <h1 class="register-title">新規登録</h1>
      <validation-observer ref="obs" v-slot="ObserverProps">
        <validation-provider v-slot="{ errors }" rules="required|max:20">
          <input v-model="name" class="name" type="text" name="name" placeholder="ユーザーネーム" />
          <div class="error">{{ errors[0] }}</div>
        </validation-provider>
        <validation-provider v-slot="{ errors }" rules="required|email">
          <input v-model="email" class="email" type="email" name="email" placeholder="メールアドレス" />
          <div class="error">{{ errors[0] }}</div>
        </validation-provider>
        <validation-provider v-slot="{ errors }" rules="required|min:8|alpha_num" vid="passwordConfirm">
          <input v-model="password" class="password" type="password" name="password" placeholder="パスワード" />
          <div class="error">{{ errors[0] }}</div>
        </validation-provider>
        <validation-provider v-slot="{ errors }" rules="confirmed:passwordConfirm">
          <input v-model="passwordConfirm" class="confirmed-password" type="password" name="passwordConfirm" placeholder="確認用パスワード" />
          <div class="error">{{ errors[0] }}</div>
        </validation-provider>
        <button @click="register" class="register-btn" :disabled="ObserverProps.invalid || !ObserverProps.validated">新規登録</button>
      </validation-observer>
      <div class="nav">
          <p class="nav-message">アカウントをお持ちの方はこちらから</p>
          <NuxtLink to="/auth/login" class="nav-link">ログイン</NuxtLink>
      </div>
    </div>
    <AuthFooter></AuthFooter>
  </div>
</template>

<script>
  import '~/assets/css/register.css'
  export default {
    auth: false,
    data() {
      return {
        name: "",
        email: "",
        password: "",
        passwordConfirm: "",
      };
    },
    methods: {
      async register() {
        const registerData = {
          name: this.name,
          email: this.email,
          password: this.password,
        };

        try {
          await this.$axios.get("sanctum/csrf-cookie");
          const url = `/api/auth/register`
          await this.$axios.post(url, registerData)
          .then(() => {
              // 新規登録に成功したら、/にページ遷移
              window.alert("新規登録に成功しました");
              this.$router.push("/auth/login");
          });
        } catch (error) {
            // 新規登録に失敗したら、コンソールに出力する
            window.alert("新規登録失敗");
            console.log(error);
        }
      },
    },
  };
</script>
