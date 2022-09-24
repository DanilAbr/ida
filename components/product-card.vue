<template>
  <div class="product-card">
    <div class="product-card__img-wrap">
      <img class="product-card__img" :src="image.url" :alt="image.alt">
    </div>

    <div class="product-card__content">
      <h3 class="product-card__title title title--l">
        {{ name }}
      </h3>
      <p class="product-card__desc">
        {{ desc }}
      </p>
      <p class="product-card__price title title--xl">
        {{ (price).toLocaleString('ru') }} руб.
      </p>
    </div>

    <button
      type="button"
      class="product-card__delete-button"
      @click="onDeleteClick"
    >
      <svg width="16" height="16" fill="none" xmlns="http://www.w3.org/2000/svg"><g clip-path="url(#a)" fill="#fff"><path d="M10.2 5.8c-.2 0-.37.16-.37.37v7.08a.37.37 0 0 0 .75 0V6.17c0-.2-.17-.37-.37-.37ZM5.79 5.8c-.21 0-.38.16-.38.37v7.08a.37.37 0 1 0 .75 0V6.17c0-.2-.17-.37-.37-.37Z" /><path d="M2.56 4.76V14c0 .54.2 1.05.55 1.42.35.37.83.58 1.34.58h7.1c.5 0 .98-.21 1.33-.58.35-.37.55-.88.55-1.42V4.76a1.43 1.43 0 0 0-.37-2.81h-1.92v-.47A1.47 1.47 0 0 0 9.66 0H6.33a1.47 1.47 0 0 0-1.48 1.48v.47H2.93a1.43 1.43 0 0 0-.37 2.81Zm8.98 10.5H4.45c-.64 0-1.14-.56-1.14-1.26V4.8h9.37V14c0 .7-.5 1.25-1.14 1.25ZM5.6 1.47a.72.72 0 0 1 .73-.73h3.33a.72.72 0 0 1 .73.73v.47H5.6v-.47ZM2.93 2.7h10.13a.67.67 0 1 1 0 1.35H2.93a.67.67 0 1 1 0-1.35Z" /><path d="M8 5.8c-.21 0-.38.16-.38.37v7.08a.37.37 0 0 0 .75 0V6.17c0-.2-.17-.37-.37-.37Z" /></g><defs><clipPath id="a"><path fill="#fff" d="M0 0h16v16H0z" /></clipPath></defs></svg>
    </button>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    id: {
      type: Number,
      required: true
    },
    image: {
      type: Object,
      default: () => {}
    },
    alt: {
      type: String,
      default: ''
    },
    name: {
      type: String,
      required: true
    },
    desc: {
      type: String,
      default: ''
    },
    price: {
      type: Number,
      required: true
    }
  },
  methods: {
    onDeleteClick () {
      this.$emit('delete-product', this.id)
    }
  }
}
</script>

<style lang="scss" scoped>
.product-card {
  position: relative;
  display: flex;
  flex-direction: column;
  height: 100%;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  &__img-wrap {
    position: relative;
    padding: percentage(200 / 332) 0 0;
  }

  &__img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  &__content {
    display: flex;
    flex-direction: column;
    height: 100%;
    padding: 16px 16px 24px;
    background: $color_white_hard;
  }

  &__title {
    margin-bottom: 16px;
  }

  &__desc {
    margin-bottom: 24px;
  }

  &__price {
    margin-top: auto;
  }

  &__delete-button {
    position: absolute;
    z-index: -1;
    top: -8px;
    right: -8px;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32px;
    height: 32px;
    padding: 0;
    opacity: 0;
    border: none;
    background: $color_red;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    cursor: pointer;
    transition: opacity 0.3s ease;
  }

  &:hover,
  &:focus {
    .product-card__delete-button {
      z-index: 0;
      opacity: 1;
    }
  }
}
</style>
