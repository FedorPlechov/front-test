<template>
  <button :disabled="disabled" class="custom-button">
    {{ content }}
  </button>
</template>

<script>
export default {
  name: 'UButton',
  props: {
    content: {
      type: String,
      required: true
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import "static/style/variables";

.custom-button {
  font-family: 'Inter', serif;
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  letter-spacing: -0.02em;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  border-radius: 10px;
  border: none;
  padding: 10px 0;
  background: #7BAE73;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  color: #FFFFFF;
  transition: background-color 200ms ease;
  &:hover {
    background-color: darkseagreen;
  }

  &:disabled {
    color: $light-gray;
    background: #EEEEEE;
    box-shadow: none;
  }
}
</style>
