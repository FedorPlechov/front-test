<template>
  <UCard class="item__container">
    <div
      class="item"
      @mouseenter="showDeleteIcon=true"
      @mouseleave="showDeleteIcon=false"
    >
      <transition>
        <div v-if="showDeleteIcon" class="item__delete-icon" @click="$emit('delete-item', item.id)" />
      </transition>
      <div :style="{backgroundImage: `url('${item.imgUrl}')`}" class="item__img" />
      <div class="item__card">
        <h3 class="item__title">
          {{ item.name }}
        </h3>
        <p class="item__description">
          {{ item.description }}
        </p>
        <p class="item__price">
          {{ (item.price).toLocaleString() }} руб.
        </p>
      </div>
    </div>
  </UCard>
</template>

<script>
export default {
  name: 'ItemProduct',
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      showDeleteIcon: false
    }
  }
}
</script>

<style lang="scss" scoped>
.item__container {
  flex: 0 0 332px;
}

.item {
  position: relative;
  display: flex;
  flex-flow: column nowrap;
  width: 100%;

  &__delete-icon {
    position: absolute;
    width: 32px;
    height: 32px;
    background-image: url("~/static/icons/delete-icon.svg");
    background-size: cover;
    top: -8px;
    right: -10px;

    &:hover {
      opacity: 0.7;
    }
  }

  &__card {
  }

  &__img {
    flex: 0 0 200px;
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
  }

  &__title {
    margin: 16px;
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
  }

  &__description {
    display: flex;
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
    margin: 16px;
    flex: 1 0 288px;
    height: 80px;
  }

  &__price {
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
    margin: 32px 16px 24px 16px;
  }
}
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
