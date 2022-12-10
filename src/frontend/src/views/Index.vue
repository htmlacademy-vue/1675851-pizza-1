<template>
  <div class="index-home">
    <header class="header">
      <div class="header__logo">
        <a href="index.html" class="logo">
          <img
            src="@/assets/img/logo.svg"
            alt="V!U!E! Pizza logo"
            width="90"
            height="40"
          />
        </a>
      </div>
      <div class="header__cart">
        <a href="cart.html">0 ₽</a>
      </div>
      <div class="header__user">
        <a href="#" class="header__login">
          <span>Войти</span>
        </a>
      </div>
    </header>

    <main class="content">
      <form action="#" method="post">
        <div class="content__wrapper">
          <h1 class="title title--big">Конструктор пиццы</h1>
          <div class="content__dough">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите тесто</h2>
              <div class="sheet__content dough">
                <label
                  v-for="(item, index) in dough"
                  :key="index"
                  class="dough__input"
                  :class="`dough__input--${getDoughValue(item.image)}`"
                >
                  <input
                    type="radio"
                    name="dough"
                    :value="`${getDoughValue(item.image)}`"
                    class="visually-hidden"
                    :checked="index === 0"
                  />
                  <b>{{ item.name }}</b>
                  <span>{{ item.description }}</span>
                </label>
              </div>
            </div>
          </div>
          <div class="content__diameter">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите размер</h2>
              <div class="sheet__content diameter">
                <label
                  v-for="(item, index) in sizes"
                  :key="index"
                  class="diameter__input"
                  :class="`diameter__input--${getSizeValue(item.multiplier)}`"
                >
                  <input
                    type="radio"
                    name="diameter"
                    :value="`${getSizeValue(item.multiplier)}`"
                    class="visually-hidden"
                    :checked="index === 0"
                  />
                  <span>{{ item.name }}</span>
                </label>
              </div>
            </div>
          </div>
          <div class="content__ingredients">
            <div class="sheet">
              <h2 class="title title--small sheet__title">
                Выберите ингредиенты
              </h2>
              <div class="sheet__content ingredients">
                <div class="ingredients__sauce">
                  <p>Основной соус:</p>
                  <label
                    v-for="(item, index) in sauces"
                    :key="index"
                    class="radio ingredients__input"
                  >
                    <input
                      type="radio"
                      name="sauce"
                      :value="`${getSauceValue(item.name)}`"
                      :checked="index === 0"
                    />
                    <span>{{ item.name }}</span>
                  </label>
                </div>
                <div class="ingredients__filling">
                  <p>Начинка:</p>
                  <ul class="ingredients__list">
                    <li
                      v-for="(item, index) in ingredients"
                      :key="index"
                      class="ingredients__item"
                    >
                      <span
                        class="filling"
                        :class="`filling--${getIngredientValue(item.image)}`"
                      >
                        {{ item.name }}
                      </span>
                      <div class="counter counter--orange ingredients__counter">
                        <button
                          type="button"
                          class="counter__button counter__button--minus"
                          disabled
                        >
                          <span class="visually-hidden">Меньше</span>
                        </button>
                        <input
                          type="text"
                          name="counter"
                          class="counter__input"
                          value="0"
                        />
                        <button
                          type="button"
                          class="counter__button counter__button--plus"
                        >
                          <span class="visually-hidden">Больше</span>
                        </button>
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
          <div class="content__pizza">
            <label class="input">
              <span class="visually-hidden">Название пиццы</span>
              <input
                type="text"
                name="pizza_name"
                placeholder="Введите название пиццы"
              />
            </label>
            <div class="content__constructor">
              <div class="pizza pizza--foundation--big-tomato">
                <div class="pizza__wrapper">
                  <div class="pizza__filling pizza__filling--ananas"></div>
                  <div class="pizza__filling pizza__filling--bacon"></div>
                  <div class="pizza__filling pizza__filling--cheddar"></div>
                </div>
              </div>
            </div>
            <div class="content__result">
              <p>Итого: 0 ₽</p>
              <button type="button" class="button" disabled>Готовьте!</button>
            </div>
          </div>
        </div>
      </form>
    </main>
  </div>
</template>

<script>
import pizza from "@/static/pizza.json";

export default {
  name: "IndexHome",
  data() {
    return {
      dough: pizza.dough,
      ingredients: pizza.ingredients,
      sauces: pizza.sauces,
      sizes: pizza.sizes,
    };
  },
  methods: {
    getDoughValue(str) {
      // eslint-disable-next-line no-useless-escape
      return str.match(/(?<=[-]).*(?=[\.])/gi)[0];
    },
    getSizeValue(multiplier) {
      switch (multiplier) {
        case 1:
          return "small";
        case 2:
          return "normal";
        case 3:
          return "big";
        default:
          return null;
      }
    },
    getSauceValue(name) {
      switch (name) {
        case "Томатный":
          return "tomato";
        case "Сливочный":
          return "creamy";
        default:
          return null;
      }
    },
    getIngredientValue(str) {
      return str.match(/[ \w-]+?(?=\.)/gi)[0];
    },
  },
};
</script>

<style lang="scss" scoped></style>
