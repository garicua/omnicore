<template>
  <button :type="typeBtn"
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
    typeBtn: {
      type: String,
      default: 'button',
    },
    disabled: Boolean,
    text: String,
    // size
    long: Boolean,
    small: Boolean,
    ml: Boolean,
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
        'button--ml': this.ml,
      };
    },
  },
  }
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/button";
</style>
