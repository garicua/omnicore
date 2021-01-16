<template>
  <header class="header">
    <h2 class="header__title">мой календарь</h2>
    <div class="header__container">
      <slot/>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/header";
</style>
