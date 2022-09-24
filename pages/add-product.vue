<template>
  <div ref="catalog" class="add-product">
    <div class="container">
      <div class="add-product__top">
        <h1 class="title title--xxl">
          Добавление товара
        </h1>

        <Select
          v-model="selectSort.value"
          :options="selectSort.options"
          :select-name="selectSort.name"
        />
      </div>

      <div class="add-product__content">
        <add-product-form
          class="add-product__form"
          @add-product="addProductCard"
        />

        <transition-group name="flip-list" tag="ul" class="add-product__product-list">
          <li
            v-for="card in sortedProductList"
            :key="card.id"
            class="add-product__product-item"
            :class="{'is-deleted': card.isDeleted}"
          >
            <product-card
              :id="card.id"
              :image="card.image"
              :name="card.name"
              :desc="card.desc"
              :price="card.price"
              @delete-product="deleteProductCard"
            />
          </li>
        </transition-group>
      </div>

      <div v-if="isLoaderShown" ref="loader" class="add-product__loader-wrapper">
        <loader />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddProduct',
  data: () => ({
    productList: [
      {
        id: 1,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 1',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10,
        isDeleted: false
      },
      {
        id: 2,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Нбименование товара 2',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 2,
        isDeleted: false
      },
      {
        id: 3,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 3',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 12,
        isDeleted: false
      },
      {
        id: 4,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 4',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 123,
        isDeleted: false
      },
      {
        id: 5,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 5',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 0,
        isDeleted: false
      },
      {
        id: 6,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 6',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 111111,
        isDeleted: false
      },
      {
        id: 7,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 1',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10,
        isDeleted: false
      },
      {
        id: 8,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Нбименование товара 2',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 2,
        isDeleted: false
      },
      {
        id: 9,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 3',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 12,
        isDeleted: false
      },
      {
        id: 10,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 4',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 123,
        isDeleted: false
      },
      {
        id: 11,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 5',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 0,
        isDeleted: false
      },
      {
        id: 12,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 6',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 111111,
        isDeleted: false
      },
      {
        id: 13,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 1',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10,
        isDeleted: false
      },
      {
        id: 14,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Нбименование товара 2',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 2,
        isDeleted: false
      },
      {
        id: 15,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 3',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 12,
        isDeleted: false
      },
      {
        id: 16,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 4',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 123,
        isDeleted: false
      },
      {
        id: 17,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 5',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 0,
        isDeleted: false
      },
      {
        id: 18,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 6',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 111111,
        isDeleted: false
      },
      {
        id: 19,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 1',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10,
        isDeleted: false
      },
      {
        id: 20,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Нбименование товара 2',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 2,
        isDeleted: false
      },
      {
        id: 21,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 3',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 12,
        isDeleted: false
      },
      {
        id: 22,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 4',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 123,
        isDeleted: false
      },
      {
        id: 23,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 5',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 0,
        isDeleted: false
      },
      {
        id: 24,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 6',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 111111,
        isDeleted: false
      },
      {
        id: 25,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 1',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10,
        isDeleted: false
      },
      {
        id: 26,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Нбименование товара 2',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 2,
        isDeleted: false
      },
      {
        id: 27,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 3',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 12,
        isDeleted: false
      },
      {
        id: 28,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 4',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 123,
        isDeleted: false
      },
      {
        id: 29,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 5',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 0,
        isDeleted: false
      },
      {
        id: 30,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 6',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 111111,
        isDeleted: false
      },
      {
        id: 31,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 1',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10,
        isDeleted: false
      },
      {
        id: 32,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Нбименование товара 2',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 2,
        isDeleted: false
      },
      {
        id: 33,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 3',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 12,
        isDeleted: false
      },
      {
        id: 34,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 4',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 123,
        isDeleted: false
      },
      {
        id: 35,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 5',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 0,
        isDeleted: false
      },
      {
        id: 36,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 6',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 111111,
        isDeleted: false
      }
    ],
    selectSort: {
      name: 'sort-select',
      value: {
        code: 1,
        name: 'По умолчанию'
      },
      options: [
        {
          code: 1,
          name: 'По умолчанию'
        },
        {
          code: 2,
          name: 'По цене min'
        },
        {
          code: 3,
          name: 'По цене max'
        },
        {
          code: 4,
          name: 'По наименованию'
        }
      ]
    },
    productShowedCount: 9,
    numberOfProductsPerPage: 9,
    isLoaderShown: true,
    requestTimeout: null,
    windowHeight: null,
    loaderHeight: null,
    headerHeight: null
  }),
  computed: {
    sortedProductList () {
      let copyList = [...this.productList]

      switch (this.selectSort.value.code) {
        case 2:
          copyList = copyList.sort((a, b) => a.price - b.price)
          break
        case 3:
          copyList = copyList.sort((a, b) => b.price - a.price)
          break
        case 4:
          copyList = copyList.sort((a, b) => a.name.localeCompare(b.name))
          break
      }

      return copyList.slice(0, this.productShowedCount)
    }
  },
  created () {
    const listFromStorage = localStorage.getItem('productList')

    if (listFromStorage) {
      this.productList = JSON.parse(listFromStorage)
      return
    }

    this.updateLocalStorage()
  },
  mounted () {
    this.windowHeight = window.innerHeight
    this.loaderHeight = this.$refs.loader?.getBoundingClientRect().height
    this.headerHeight = document.querySelector('.header')?.getBoundingClientRect().height
    this.onScroll()
    window.addEventListener('scroll', this.onScroll)
  },
  unmounted () {
    window.removeEventListener('scroll', this.onScroll)
  },
  methods: {
    deleteProductCard (id) {
      this.productList.find(product => product.id === id).isDeleted = true

      setTimeout(() => {
        this.productList = this.productList.filter(product => product.id !== id)
        this.updateLocalStorage()
      }, 300)
    },
    addProductCard ({ name, desc, url, price }) {
      const isNotUniq = this.productList.find((product) => {
        return product.name === name && product.desc === desc && product.image.url === url && product.price === price
      })

      if (!isNotUniq) {
        this.productList.push({
          id: this.productList.length + 1,
          image: {
            url,
            alt: ''
          },
          name,
          desc,
          price
        })

        this.updateLocalStorage()
        this.$toast.success('Товар успешно добавлен')
      } else {
        this.$toast.error('Такой товар уже был добавлен')
      }
    },
    updateLocalStorage () {
      localStorage.setItem('productList', JSON.stringify(this.productList))
    },
    onScroll () {
      if (this.productShowedCount > this.productList.length) {
        return
      }

      const catalogBottom = this.$refs.catalog?.getBoundingClientRect().bottom

      if (Math.floor(catalogBottom) <= this.windowHeight + this.headerHeight + this.loaderHeight) {
        this.updateList()
      }
    },
    updateList () {
      // для имитации запроса с бэка
      this.requestTimeout = clearTimeout(this.requestTimeout)
      this.requestTimeout = setTimeout(() => {
        this.productShowedCount += this.numberOfProductsPerPage

        if (this.productShowedCount >= this.productList.length) {
          this.isLoaderShown = false
        }
      }, 700)
    }
  }
}
</script>

<style lang="scss" scoped>
.add-product {
  min-height: 100vh;
  padding: 32px 0;
  background: $color_grey-light;

  @media (max-width: 767px) {
    padding: 24px 0;
  }

  &__top {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 16px;
  }

  &__content {
    display: grid;
    gap: 0 16px;
    grid-template-columns: repeat(16, 1fr);

    @media (max-width: 767px) {
      display: block;
    }
  }

  &__form {
    height: max-content;
    grid-column: 1 / 5;

    @media (max-width: 1279px) {
      grid-column: 1 / 7;
    }

    @media (max-width: 767px) {
      margin-bottom: 24px;
    }
  }

  &__product-list {
    display: grid;
    gap: 16px;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    grid-column: 5 / -1;

    @media (max-width: 1279px) {
      grid-column: 7 / -1;
    }
  }

  &__product-item {
    &.is-deleted {
      transform: scale(0);
      transition: transform 0.7s ease;
    }
  }

  &__loader-wrapper {
    position: relative;
    width: 100%;
    height: 300px;
  }

  .flip-list-move {
    transition: transform 1s;
  }
}
</style>
