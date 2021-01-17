<template>
  <label class="input-text__label">
    <input class="input-text"
           type="text"
           :placeholder="placeholder"
           @input="input"
    />
  </label>
</template>

<script>
  export default {
    name: "InputText",
    props: {
      placeholder: String,
    },
    methods: {
      input(event) {
        this.$emit('input', event.target.value);
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/input-text";
</style>
