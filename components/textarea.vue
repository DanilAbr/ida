<template>
  <div class="textarea">
    <span class="textarea__label">
      {{ label }}
    </span>
    <textarea
      class="textarea__field"
      :value="value"
      :maxlength="maxLength"
      :name="name"
      :placeholder="placeholder"
      @input="$emit('input', $event.target.value)"
    />
  </div>
</template>

<script>
export default {
  name: 'TextareVue',
  props: {
    name: {
      type: String,
      default: ''
    },
    label: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    },
    maxLength: {
      type: Number,
      default: 255
    },
    placeholder: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss">
.textarea {
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
    height: 125px;
    padding: 10px 16px 11px 10px;
    color: $color_black;
    font-family: inherit;
    font-size: 12px;
    line-height: 15px;
    border: none;
    border-radius: 4px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    resize: none;

    &::placeholder {
      color: $color_grey-dark;
    }

    &:focus,
    &:hover {
      background: $color_grey-light;
    }
  }
}
</style>
