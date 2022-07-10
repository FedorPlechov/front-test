<template>
  <UCard class="card">
    <form ref="form" class="item-form" @submit.prevent="submit">
      <UInput
        id="item-name"
        v-model="item.name"
        :required="true"
        label="Наименование"
        placeholder="Введите наименование товара"
        type="text"
      />
      <UTextArea
        id="item-description"
        v-model="item.description"
        :cols="37"
        :rows="6"
        label="Описание товара"
        placeholder="Введите описание товара"
      />
      <UInput
        id="img-url"
        v-model="item.imgUrl"
        :required="true"
        label="Ссылка на изображение товара"
        placeholder="Введите ссылку"
        type="text"
      />
      <UInput
        id="item-price"
        v-model="item.price"
        v-mask="currencyMask"
        :required="true"
        label="Цена товара"
        placeholder="Введите цену"
        type="text"
      />
      <UButton content="Добавить товар" :disabled="!formIsValid" />
    </form>
  </UCard>
</template>

<script>
import createNumberMask from 'text-mask-addons/dist/createNumberMask'
import { createId } from '@/service/create-id'

const currencyMask = createNumberMask({
  prefix: '',
  allowDecimal: false,
  includeThousandsSeparator: true,
  thousandsSeparatorSymbol: ' ',
  allowNegative: false
})

export default {
  name: 'ItemForm',
  data () {
    return {
      currencyMask,
      item: {
        name: '',
        description: '',
        imgUrl: '',
        price: ''
      },
      requiredFields: ['name', 'imgUrl', 'price']
    }
  },
  computed: {
    formIsValid () {
      return this.requiredFields.every(field => (this.item[field] && this.item[field].trim() !== ''))
    }
  },
  methods: {
    submit () {
      const id = createId()
      const item = {
        id,
        ...this.item
      }
      this.$emit('add-item', item)
      this.$refs.form.reset()
    }
  }
}
</script>

<style lang="scss" scoped>
.item-form {
  padding: 1.5rem 1.5rem 0 1.5rem ;
  width: 100%;
  box-sizing: border-box;
  @media (max-width: 770px) {
    min-width: 332px;
  }

  &:deep(.custom-input) {
    margin-bottom: 10px;
    &:last-of-type {
      margin-bottom: 18px;
    }
  }

  &:deep(.custom-input .custom-input__text-area) {
    margin-bottom: 10px;
  }
  &:last-child {
    margin-bottom: 24px;
  }
}

.card {
  position: sticky;
  margin-right: 16px;
  top: 0;
  max-height: 440px;
  max-width: 332px;
  @media (max-width: 770px) {
    position: static;
    margin: 0 auto 1rem auto;
  }
}
</style>
