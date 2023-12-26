<template>
  <div class="register">
    <AuthHeader></AuthHeader>
    <div class="register__container">
      <h1 class="register-title">新規登録</h1>
      <input v-model="name" class="name" type="text" name="name" placeholder="ユーザーネーム" />
      <input v-model="email" class="email" type="email" name="email" placeholder="メールアドレス" />
      <input v-model="password" class="password" type="password" name="password" placeholder="パスワード" />
      <button @click="register" class="register-btn">新規登録</button>
    </div>
  </div>
</template>

<script>
export default {
  auth: false,
  data() {
    return {
      name: "",
      email: "",
      password: "",
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
