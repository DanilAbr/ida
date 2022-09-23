<template>
  <button
    :type="type"
    :disabled="disabled"
    class="button"
    @click="$emit('on-click')"
  >
    {{ label }}
  </button>
</template>

<script>
export default {
  name: 'ButtonVue',
  props: {
    type: {
      type: String,
      default: 'submit'
    },
    label: {
      type: String,
      required: true
    },
    disabled: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
.button {
  padding: 10px 0 11px;
  font-family: inherit;
  font-size: 12px;
  line-height: 15px;
  color: white;
  width: 100%;
  background: $color_green;
  border: none;
  border-radius: 10px;
  cursor: pointer;

  &:disabled {
    color: $color_grey-dark;
    background: $color_grey;
  }

  &:focus,
  &:hover {
    opacity: 0.7;
  }

  &:active {
    opacity: 0.5;
  }
}
</style>
