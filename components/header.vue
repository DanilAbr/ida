<template>
  <header class="header">
    <nav class="container">
      <ul class="header__menu-list">
        <li
          v-for="link in links"
          :key="link.id"
        >
          <nuxt-link :to="link.url" class="header__link">
            {{ link.name }}
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'HeaderVue',
  data: () => ({
    links: [
      {
        id: 1,
        name: 'Главная',
        url: '/'
      },
      {
        id: 2,
        name: 'Добавление товара',
        url: '/add-product'
      },
      {
        id: 3,
        name: 'Количество потраченного времени на сайт',
        url: '/amount-of-time-spent'
      }
    ]
  })
}
</script>

<style lang="scss">
.header {
  min-height: 40px;
  background: $color_grey-light;
  border-bottom: 2px solid $color_grey;

  &__menu-list {
    display: flex;
  }

  &__link {
    display: inline-block;
    padding: 10px 16px;
    font-family: inherit;
    text-decoration: none;
    border-radius: 3px;
    transition: background 0.2s ease / opacity 0.2 ease;

    &:hover,
    &:focus {
      background: $color_grey;
    }

    &:active {
      color: inherit;
      opacity: 0.7;
    }
  }
}
</style>
