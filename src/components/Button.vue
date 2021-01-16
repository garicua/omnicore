<template>
  <button type="button"
          class="button"
          :class="classes"
          :disabled="disabled"
          v-on="$listeners"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    disabled: Boolean,
    text: String,
    // size
    long: Boolean,
    small: Boolean,
    // color
    primary: Boolean,
    secondary: Boolean,
  },
  computed: {
    classes() {
      return {
        'button--long': this.long,
        'button--small': this.small,
        'button--primary': this.primary,
        'button--secondary': this.secondary,
      };
    },
  },
  }
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/button";
</style>
