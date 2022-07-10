<template>
  <div class="custom-input">
    <label
      :for="id"
      class="custom-input__label"
    >
      {{ label }}
      <span
        v-if="required"
        class="custom-input__label_required"
      />
    </label>
    <textarea
      :id="id"
      v-model="model"
      :style="{
        maxWidth, maxHeight
      }"
      :cols="cols"
      :placeholder="placeholder"
      :rows="rows"
      class="custom-input__text-area"
    />
  </div>
</template>

<script>
export default {
  name: 'UTextArea',
  props: {
    id: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    value: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      required: true
    },
    rows: {
      type: Number,
      required: true
    },
    cols: {
      type: Number,
      required: true
    },
    maxWidth: {
      type: String,
      required: false,
      default: '17rem'
    },
    maxHeight: {
      type: String,
      required: false,
      default: '6.9rem'
    },
    required: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    model: {
      get () {
        return this.value
      },
      set (value) {
        this.$emit('input', value)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import "static/style/variables";

.custom-input {
  display: flex;
  flex-flow: column;

  &__label {
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;

    &_required {
      position: absolute;
      width: 4px;
      height: 4px;
      background: #FF8484;
      border-radius: 100%;
    }
  }

  &__text-area {
    border: none;
    background: #FFFEFB;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    padding: 10px 16px;
    min-height: 2.5rem;
  }
}
</style>
