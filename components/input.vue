<template>
  <div class="input">
    <span v-if="label" class="input__label">
      {{ label }}
    </span>
    <input
      class="input__field"
      :value="value"
      :type="type"
      :name="name"
      :placeholder="placeholder"
      @input.stop="$emit('input', $event.target.value)"
    >
    <span v-if="error" class="input__error">
      {{ error }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'InputVue',
  props: {
    label: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    name: {
      type: String,
      required: true
    },
    error: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss">
.input {
  display: flex;
  flex-direction: column;

  &__label {
    color: $color_black-light;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    margin-bottom: 4px;
  }

  &__field {
    padding: 10px 16px 11px 10px;
    color: $color_black;
    font-family: inherit;
    font-size: 12px;
    line-height: 15px;
    border: none;
    border-radius: 4px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);

    &::placeholder {
      color: $color_grey-dark;
    }

    &:focus,
    &:hover {
      background: $color_grey-light;
    }
  }

  &__error {
    font-size: 14px;
    line-height: 20px;
    color: $color_red;
  }
}
</style>
