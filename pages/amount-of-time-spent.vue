<template>
  <div class="amount-of-time-spent">
    <div class="container">
      <h1 class="title title--xxl">
        {{ pageTitle }}.<br><span v-if="totalHours">Всего {{ totalHours }} час(а/ов)</span>
      </h1>

      <table class="amount-of-time-spent__table">
        <thead>
          <td>Краткое описание задачи</td>
          <td>Количество потраченных часов</td>
        </thead>
        <tr
          v-for="task in tasks"
          :key="task.id"
        >
          <td v-html="task.label" />
          <td>
            {{ task.hours }}
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AmountOfTimeSpent',
  data () {
    // свойство будет нереактивным
    this.pageTitle = 'Количество потраченного времени'

    return {
      tasks: [
        {
          id: 1,
          label: 'Настройка проекта, подключение к гиту',
          hours: 1
        },
        {
          id: 2,
          label: 'Добавление и настройка страницы "Количество потраченного времени"',
          hours: 1
        },
        {
          id: 3,
          label: 'Вёрстка формы для добавления товара<br>Добавление компонентов Input, Textarea, Button"',
          hours: 1
        },
        {
          id: 4,
          label: 'Вёрстка карточек товара + расположение их по сетке',
          hours: 1
        },
        {
          id: 5,
          label: 'Добавление селекта, кнопки удаления, состояний интерактивных элементов',
          hours: 1
        },
        {
          id: 6,
          label: 'Создание адаптива на всех страницах. Настройка и создание меню для мобильного разрешения',
          hours: 1
        },
        {
          id: 6,
          label: 'Добавление кастомной валидации на форму добавления товара',
          hours: 1.5
        },
        {
          id: 7,
          label: 'Настройка функционала добавления товара, правки в карточке товара',
          hours: 0.5
        }
      ]
    }
  },
  computed: {
    totalHours () {
      return this.tasks.map(task => task.hours).reduce((a, b) => +a + +b, 0)
    }
  }
}
</script>

<style lang="scss" scoped>
.amount-of-time-spent {
  padding: 32px 0;
  min-height: 100vh;

  @media (max-width: 767px) {
    padding: 24px 0;
  }

  &__table {
    width: 50%;
    margin-top: 16px;
    box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    @media (max-width: 767px) {
      width: 100%;
    }

    thead {
      background: $color_grey-light;
    }

    td {
      padding: 10px 16px 12px;
      border: 1px solid $color_grey;
    }
  }
}
</style>
