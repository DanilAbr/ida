<template>
  <form class="add-product-form">
    <Input
      v-model.trim="form.inputName.value"
      :label="form.inputName.label"
      :placeholder="form.inputName.placeholder"
      :name="form.inputName.name"
      :error="form.inputName.error"
    />

    <Textarea
      v-model.trim="form.textareaDesc.value"
      :label="form.textareaDesc.label"
      :placeholder="form.textareaDesc.placeholder"
      :name="form.textareaDesc.name"
    />

    <Input
      v-model.trim="form.inputImageUrl.value"
      :label="form.inputImageUrl.label"
      :placeholder="form.inputImageUrl.placeholder"
      :name="form.inputImageUrl.name"
      :error="form.inputImageUrl.error"
    />

    <Input
      v-model.trim="form.inputProductPrice.value"
      :label="form.inputProductPrice.label"
      :placeholder="form.inputProductPrice.placeholder"
      :name="form.inputProductPrice.name"
      :error="form.inputProductPrice.error"
      only-numbers
      separated
    />

    <Button
      class="add-product-form__add-product-button"
      :label="'Добавить товар'"
      :disabled="!isFormValid"
      type="button"
      @on-click="onAddProductClick"
    />
  </form>
</template>

<script>
export default {
  name: 'AddProductForm',
  data: () => ({
    errors: {
      required: 'Это обязательное поле'
    },
    form: {
      inputName: {
        value: '',
        label: 'Наименование товара',
        placeholder: 'Введите наименование товара',
        name: 'name-add-product',
        error: '',
        touched: false
      },
      inputImageUrl: {
        value: '',
        label: 'Ссылка на изображение товара',
        placeholder: 'Введите ссылку',
        name: 'img-url-add-product',
        error: '',
        touched: false
      },
      inputProductPrice: {
        value: '',
        label: 'Цена товара',
        placeholder: 'Введите цену',
        name: 'cost-add-product',
        error: '',
        touched: false
      },
      textareaDesc: {
        value: '',
        label: 'Описание товара',
        placeholder: 'Введите наименование товара',
        name: 'description-add-product'
      }
    },
    requestTimeout: null,
    isFormValid: false
  }),
  watch: {
    form: {
      handler () {
        this.requestTimeout = clearTimeout(this.requestTimeout)
        this.requestTimeout = setTimeout(() => {
          this.validateForm()
        }, 300)
      },
      deep: true
    }
  },
  methods: {
    validateForm () {
      const { inputName, inputImageUrl, inputProductPrice } = this.form

      this.setTouchedStateOnField(inputName)
      this.setTouchedStateOnField(inputImageUrl)
      this.setTouchedStateOnField(inputProductPrice)

      this.setRequiredErrorOnField(inputName)
      this.setRequiredErrorOnField(inputImageUrl)
      this.setRequiredErrorOnField(inputProductPrice)

      this.isFormValid = !!(inputName.value && inputImageUrl.value && inputProductPrice.value)
    },
    setRequiredErrorOnField (field) {
      field.error = !field.value && field.touched ? this.errors.required : ''
    },
    setTouchedStateOnField (field) {
      if (field.value) {
        field.touched = true
      }
    },
    onAddProductClick () {
      this.$emit('add-product', {
        name: this.form.inputName.value,
        desc: this.form.textareaDesc.value,
        url: this.form.inputImageUrl.value,
        price: +this.form.inputProductPrice.value.replace(/\s+/g, '')
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.add-product-form {
  display: flex;
  flex-direction: column;
  gap: 16px 0;
  padding: 24px;
  background: $color_white-hard;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  &__add-product-button {
    margin-top: 8px;
  }
}
</style>
