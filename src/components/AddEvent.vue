<template>
  <div>
    <div class="add-event">
      <div class="add-event__header">
        <div class="add-event__title">Введите событие на {{ data }}</div>
        <div class="add-event__close" @click="click">x</div>
      </div>
      <div class="add-event__body">
        <slot/>
      </div>
    </div>
    <div class="add-event__overlay" @click="click"></div>
  </div>
</template>

<script>
  export default {
    name: "AddEvent",
    props: {
      data: String,
    },
    methods: {
      click() {
        this.$emit('click');
      },
    },
  }
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/add-event";
</style>
