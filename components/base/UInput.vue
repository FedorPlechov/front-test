<template>
  <div class="custom-input">
    <label
      :for="id"
      class="custom-input__label"
    >{{ label }}
      <span
        v-if="required"
        class="custom-input__label_required"
      />
    </label>
    <input
      :id="id"
      ref="input"
      v-model="model"
      :name="id"
      :placeholder="placeholder"
      class="custom-input__input"
      :class="{['custom-input__input_invalid']: isInvalid}"
      :type="type"
      @focus="clearValidity"
    >
    <span :class="{['error-message_invalid']:isInvalid}" class="error-message">Это поле обязательно</span>
  </div>
</template>

<script>
export default {
  name: 'UInput',
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
      type: [String, Number],
      required: true
    },
    placeholder: {
      type: String,
      required: true
    },
    type: {
      type: String,
      required: true
    },
    required: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  data () {
    return {
      isInvalid: false
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
  },
  mounted () {
    if (this.required) {
      this.$refs.input.addEventListener('blur', (event) => {
        this.isInvalid = !(event.target.value && event.target.value.trim() !== '')
      })
    }
  },
  methods: {
    clearValidity () {
      this.isInvalid = false
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

  &__input {
    border: none;
    background: #FFFEFB;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    padding: 10px 16px;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;

    ::placeholder {
      color: $light-gray;
    }
    &_invalid {
      border: 1px solid #FF8484;
    }
  }
}
.error-message {
  font-weight: 400;
  font-size: 8px;
  line-height: 10px;
  letter-spacing: -0.02em;
  color: #FF8484;
  opacity: 0;
  transition: opacity 0.15s ease-in-out;
  transform: translateY(4px);
  &_invalid {
    opacity: 1;
  }
}
</style>
