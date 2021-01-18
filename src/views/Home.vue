<template>
  <div class="home">
    <div class="home__logo">
      <img alt="Vue logo" src="../assets/logo.png">
    </div>
    <router-link to="/calendar"  class="home__link">
      show calendar by vue
      <span v-for="i in 3" :key="i" class="home__dots">.</span>
    </router-link>
  </div>
</template>

<script>

export default {
  name: 'Home',
};
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/home";
</style>
