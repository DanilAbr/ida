<template>
  <div class="product-card">
    <img class="product-card__img" :src="image.url" :alt="image.alt">

    <div class="product-card__content">
      <h3 class="product-card__title title title--l">
        {{ label }}
      </h3>
      <p>{{ desc }}</p>
      <p class="product-card__price title title--xl">
        {{ price }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    image: {
      type: Object,
      default: () => {}
    },
    alt: {
      type: String,
      default: ''
    },
    label: {
      type: String,
      required: true
    },
    desc: {
      type: String,
      default: ''
    },
    price: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss" scoped>
.product-card {
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  overflow: hidden;

  &__img {
    display: block;
    width: 100%;
  }

  &__content {
    padding: 16px 16px 24px;
    background: $color_white_hard;
  }

  &__title {
    margin-bottom: 16px;
  }

  &__price {
    margin-top: 24px;
  }
}
</style>
