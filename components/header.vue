<template>
  <header class="header">
    <div class="container">
      <nav class="header__nav" :class="{'is-showed': isMenuShowed}">
        <ul class="header__menu-list">
          <li
            v-for="link in links"
            :key="link.id"
            class="header__menu-item"
          >
            <button type="button" :to="link.url" class="header__link" @click="onLinkClick(link.url)">
              {{ link.name }}
            </button>
          </li>
        </ul>

        <button
          class="header__button-toggle-menu"
          type="button"
          :aria-label="isMenuShowed ? 'Закрыть меню' : 'Открыть меню'"
          @click="onToggleMenuClick"
        />
      </nav>
    </div>
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
    ],
    isMenuShowed: false
  }),
  methods: {
    toggleMenu () {
      this.isMenuShowed = !this.isMenuShowed
    },
    onToggleMenuClick () {
      this.toggleMenu()
    },
    onLinkClick (url) {
      if (this.isMobile()) {
        this.toggleMenu()
      }
      this.$router.push(url)
    },
    isMobile () {
      return window.innerWidth < 767
    }
  }
}
</script>

<style lang="scss">
.header {
  min-height: 40px;
  background: $color_grey-light;
  border-bottom: 2px solid $color_grey;

  &__nav {
    @media (max-width: 767px) {
      position: absolute;
      max-width: calc(100vw - 40px);
      background: $color_white-hard;
      box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
      border-radius: 4px;
      transform: translate3d(calc(-100% - 40px), 0, 0);
      transition: transform 0.7s ease;

      &.is-showed {
        transform: translate3d(-16px, 0, 0);

        .header__button-toggle-menu {
          &::after {
            transform: rotate(-45deg);
          }

          &::before {
            transform: rotate(45deg);
          }
        }
      }
    }
  }

  &__menu-list {
    display: flex;
    flex-wrap: wrap;

    @media (max-width: 767px) {
      display: block;
    }
  }

  &__link {
    display: inline-block;
    padding: 10px 16px;
    color: inherit;
    font-family: inherit;
    font-size: inherit;
    text-align: left;
    text-decoration: none;
    border-radius: 3px;
    transition: background 0.2s ease / opacity 0.2 ease;
    border: none;
    background: transparent;
    cursor: pointer;

    &:hover,
    &:focus {
      background: $color_grey;
    }

    &:active {
      color: inherit;
      opacity: 0.7;
    }

    @media (max-width: 767px) {
      width: 100%;
    }
  }

  &__button-toggle-menu {
    display: none;

    @media (max-width: 767px) {
      position: absolute;
      top: 0;
      display: block;
      right: 0;
      width: 40px;
      height: 40px;
      cursor: pointer;
      background: transparent;
      border: none;
      transform: translate3d(30px, 0, 0);

      &::after,
      &::before {
        content: '';
        position: absolute;
        width: 24px;
        height: 2px;
        background: $color_black-light;
        transition: transform 0.3s ease;
      }

      &::after {
        transform: rotate(0) translate3d(40px, 4px, 0);
      }

      &::before {
        transform: rotate(0) translate3d(40px, -4px, 0);
      }
    }
  }
}
</style>
