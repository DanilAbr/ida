<template>
  <form class="add-product-form">
    <Input
      :label="'Наименование товара'"
      :placeholder="'Введите наименование товара'"
      :name="'name-add-product'"
    />

    <Textarea
      :label="'Описание товара'"
      :placeholder="'Введите наименование товара'"
      :name="'description-add-product'"
    />

    <Input
      :label="'Ссылка на изображение товара'"
      :placeholder="'Введите ссылку'"
      :name="'img-url-add-product'"
    />

    <Input
      :label="'Цена товара'"
      :placeholder="'Введите цену'"
      :name="'cost-add-product'"
    />

    <Button
      class="add-product-form__submit-button"
      :label="'Добавить товар'"
      :disabled="false"
    />
  </form>
</template>

<style lang="scss" scoped>
.add-product-form {
  display: flex;
  flex-direction: column;
  gap: 16px 0;
  padding: 24px;
  background: $color_white-hard;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  &__submit-button {
    margin-top: 8px;
  }
}
</style>
