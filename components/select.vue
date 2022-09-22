<template>
  <select class="select" :name="selectName">
    <option
      v-for="option in options"
      :key="option.code"
      :value="option.name"
    >
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'SelectVue',
  props: {
    value: {
      type: Object,
      default: () => {}
    },
    options: {
      type: Array,
      required: true
    },
    selectName: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.select {
  padding: 10px 12px 11px 16px;
  color: $color_grey-dark;
  font-family: inherit;
  font-size: 12px;
  line-height: 15px;
  border: none;
  background-color: $color_white-hard;
  background-image: url('/svg/dropdown-icon.svg');
  background-repeat: no-repeat;
  background-position: right 16px top 14px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  appearance: none;
  cursor: pointer;

  &:hover,
  &:focus {
    background-color: $color_grey-light;
  }

  &:active {
    color: inherit;
    opacity: 0.7;
  }
}
</style>
