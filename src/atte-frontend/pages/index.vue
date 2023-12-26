<template>
<div>
  <AuthHeader></AuthHeader>
  <h1>ログインしました</h1>
  <p>{{ $auth.loggedIn }}</p>
  <p>{{ $auth.user }}</p>
</div>
</template>

<script>
export default {
}
</script>
