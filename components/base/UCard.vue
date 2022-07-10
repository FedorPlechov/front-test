<template>
  <div class="card">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'UCard'
}
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  background: rgba(255, 254, 251, 1);
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04),
  0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  min-width: 332px;
  transition: transform 500ms ease;
  &:hover {
    cursor: pointer;
  }
}
</style>
