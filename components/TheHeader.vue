<template>
  <div class="header">
    <div class="header__title">
      <h2>Добавление товара</h2>
    </div>
    <div class="header__sort">
      <USelect :default="defaultSort" :options="sortOptions" @input="selectHandler($event)" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheHeader',
  computed: {
    defaultSort () {
      return { name: 'По умолчанию', id: 'byDefault' }
    },
    sortOptions () {
      return [
        { name: 'По цене min', id: 'asc' },
        { name: 'По цене max', id: 'desc' },
        { name: 'По наименованию', id: 'byName' }
      ]
    }
  },
  methods: {
    selectHandler (payload) {
      this.$emit('sort', payload)
    }
  }
}
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  width: 100%;
  justify-content: space-between;
  @media (max-width: 770px){
   justify-content: center;
  }
  &__title {
    @media (max-width: 770px){
      flex: 0 1 245px;
    }
  }

  &__title h2 {
    font-size: 1.75rem;
    font-weight: 600;
    line-height: 35px;
    margin: 9px 0 0 0;
  }
  &__sort {
    @media (max-width: 770px){
      margin-top: 1rem;
    }
  }
}
</style>
