<template>
  <div class="calendar-navigation">
    <div class="calendar-navigation__container">
      <slot/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalendarNavigation',
};
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/calendar-navigation";
</style>
