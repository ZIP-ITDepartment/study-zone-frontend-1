<template>
  <h3>Redirecting...</h3>
</template>

<script>
  export default {
    mounted () {
      this.$router.push('/client/auth/login');
    }
  }
</script>
