<template>
  <main class="container">
    <ItemForm @add-item="addItem($event)" />
    <ListOfItems :items="sortedItems" @delete-item="deleteItem($event)" />
  </main>
</template>

<script>
export default {
  name: 'TheMain',
  props: {
    sortParameter: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      items: []
    }
  },
  computed: {
    sortedItems () {
      const items = this.items
      switch (this.sortParameter) {
        case 'asc' :
          return items.sort((a, b) => {
            return +a.price.replace(/\s+/g, '') - +b.price.replace(/\s+/g, '')
          })
        case 'desc' :
          return items.sort((a, b) => (+b.price.replace(/\s+/g, '')) - (+a.price.replace(/\s+/g, '')))
        case 'byName' :
          return items.sort((a, b) => {
            return a.name.localeCompare(b.name)
          })
        default :
          return items
      }
    }
  },
  mounted () {
    this.items = JSON.parse(localStorage.getItem('items'))
  },
  updated () {
    this.saveToLocaleStorage()
  },
  methods: {
    addItem (item) {
      this.items.unshift(item)
    },
    deleteItem (id) {
      this.items = this.items.filter(item => item.id !== id)
    },
    saveToLocaleStorage () {
      localStorage.setItem('items', JSON.stringify(this.items))
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  margin-top: 1rem;
  padding-bottom: 1rem;
  @media (max-width: 770px) {
    flex-direction: column;
  }
}
</style>
