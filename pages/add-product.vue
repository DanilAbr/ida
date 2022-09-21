<template>
  <div class="add-product">
    <div class="container">
      <h1 class="add-product__title title title--xxl">
        Добавление товара
      </h1>

      <div class="add-product__content">
        <add-product-form class="add-product__form" />

        <ul class="add-product__product-list">
          <li
            v-for="card in productList"
            :key="card.id"
            class="add-product__product-item"
          >
            <product-card
              :image="card.image"
              :label="card.label"
              :desc="card.desc"
              :price="card.price"
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
        label: 'Наименование товара',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000 руб.'
      },
      {
        id: 2,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        label: 'Наименование товара',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000 руб.'
      },
      {
        id: 3,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        label: 'Наименование товара',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000 руб.'
      },
      {
        id: 4,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        label: 'Наименование товара',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000 руб.'
      },
      {
        id: 5,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        label: 'Наименование товара',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000 руб.'
      },
      {
        id: 6,
        image: {
          url: 'https://loremflickr.com/332/200',
          alt: ''
        },
        label: 'Наименование товара',
        desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000 руб.'
      }
    ]
  })
}
</script>

<style lang="scss" scoped>
.add-product {
  min-height: 100vh;
  padding: 32px 0;
  background: $color_grey-light;

  &__title {
    margin-bottom: 16px;
  }

  &__content {
    display: grid;
    grid-template-columns: repeat(16, 1fr);
    gap: 0 16px;
  }

  &__form {
    height: max-content;
    grid-column: 1 / 5;
  }

  &__product-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    grid-column: 5 / -1;
  }
}
</style>
