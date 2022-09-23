<template>
  <div class="add-product">
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

        <ul class="add-product__product-list">
          <li
            v-for="card in sortedProductList"
            :key="card.id"
            class="add-product__product-item"
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
        </ul>
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
        price: 10
      },
      {
        id: 2,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Нбименование товара 2',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 2
      },
      {
        id: 3,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 3',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 12
      },
      {
        id: 4,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 4',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 123
      },
      {
        id: 5,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 5',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 0
      },
      {
        id: 6,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        name: 'Наименование товара 6',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 111111
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
    }
  }),
  computed: {
    sortedProductList () {
      const copyList = [...this.productList]

      switch (this.selectSort.value.code) {
        case 2:
          return copyList.sort((a, b) => a.price - b.price)
        case 3:
          return copyList.sort((a, b) => b.price - a.price)
        case 4:
          return copyList.sort((a, b) => a.name.localeCompare(b.name))
        default:
          return copyList
      }
    }
  },
  methods: {
    deleteProductCard (id) {
      this.productList = this.productList.filter(product => product.id !== id)
    },
    addProductCard ({ name, desc, url, price }) {
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

      this.$toast.success('Товар успешно добавлен')
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
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    grid-column: 5 / -1;

    @media (max-width: 1279px) {
      grid-column: 7 / -1;
    }
  }
}
</style>
