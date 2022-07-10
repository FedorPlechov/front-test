<template>
  <div :tabindex="tabindex" class="custom-select" @blur="open = false">
    <div :class="{ open: open }" class="selected" @click="open = !open">
      {{ selected.name }}
    </div>
    <div :class="{ selectHide: !open }" class="items">
      <div
        v-for="(option, i) of options"
        :key="i"
        @click="
          selected = option;
          open = false;
          $emit('input', option.id);
        "
      >
        {{ option.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'USelect',
  props: {
    options: {
      type: Array,
      required: true
    },
    default: {
      type: Object,
      required: false,
      default: null
    },
    tabindex: {
      type: Number,
      required: false,
      default: 0
    }
  },
  data () {
    return {
      selected: this.default
        ? this.default
        : this.options.length > 0
          ? this.options[0]
          : null,
      open: false
    }
  },
  mounted () {
    this.$emit('input', this.selected.id)
  }
}
</script>

<style lang="scss" scoped>
@import 'static/style/variables';
.custom-select {
  position: relative;
  width: 100%;
  min-width: 122px;
  text-align: left;
  outline: none;
  height: 36px;
  line-height: 15px;
  font-size: 12px;
  font-weight: 400;
}

.custom-select .selected {
  box-sizing: border-box;
  color: $light-gray;
  padding: 0.6rem 1rem;
  cursor: pointer;
  user-select: none;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.custom-select .selected.open {
  border-radius: 6px 6px 0 0;
}

.custom-select .selected:after {
  content: "";
  border: solid $light-gray;
  border-width: 0 2px 2px 0;
  display: inline-block;
  padding: 3px;
  transform: translateY(-1px) rotate(45deg);
  margin-left: 5px;
}

.custom-select .items {
  color: #fff;
  overflow: hidden;
  position: absolute;
  left: 0;
  right: 0;
  z-index: 1;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.custom-select .items div {
  color: $light-gray;
  padding: 0.8em;
  cursor: pointer;
  user-select: none;
}

.custom-select .items div:hover {
  background-color: $light-gray;
  color: $base-color;
}

.selectHide {
  display: none;
}
</style>
