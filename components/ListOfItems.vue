<template>
  <transition-group v-if="items.length > 0" class="items" tag="div" name="card">
    <Item v-for="item in items" :key="item.id" :item="item" class="card" @delete-item="$emit('delete-item', $event)" />
  </transition-group>
  <UPreloader v-else />
</template>

<script>
export default {
  name: 'ListOfItems',
  props: {
    items: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.items {
  display: flex;
  max-width: 1028px;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1rem;
  @media (max-width:1427px) {
    justify-content: center;
  }
}
.card {
  transition: all 0.5s;
}
.card-enter, .card-leave-to
   {
  opacity: 0;
  transform: scale(0);
}
.card-enter-to {
  opacity: 1;
  transform: scale(1);
}
.card-move {
  transition: all 1s;
}
@keyframes slide-in {
  from {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
