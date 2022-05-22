<template>
  <div class="profile">
    <p class="profile__username">{{ username }}</p>

    <ul class="profile__list info-list">
      <li>Тривио</li>
      <li>Баланс: {{ balanceFormatted }} &#8381;</li>
      <li>Задолженность: {{ debtFormatted }} &#8381;</li>
    </ul>

    <ul class="profile__list btns-list">
      <li v-for="btn of buttons">
        <a href="#" :class="`btns-list__link ${btn === `Выйти` ? `btns-list__link_logout` : ``}`">
          {{ btn }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    username: String,
  },

  data() {
    return {
      buttons: ["Профиль", "Управление", "Моя компания", "Выйти"],
      balance: -568978.25,
      debt: 0
    };
  },

  methods: {
    formatSum(num) {
      return num
        ? num.toString().replace(/\./, ",")
        : "0,00";
    },
  },

  computed: {
    balanceFormatted() {
      return this.formatSum(this.balance);
    },
    debtFormatted() {
      return this.formatSum(this.debt);
    },
  },
};
</script>

<style lang="scss">
@import "src/styles/main.scss";

%text-second {
  font-size: 0.75rem;
  color: $normal-gray;
}

.profile {
  position: absolute;
  top: calc(100% + 24px);
  right: 0;

  min-width: 250px;
  padding: 16px 20px;

  border-radius: 8px;
  background-color: white;
  -webkit-box-shadow: -1px 4px 16px 7px rgba(118, 121, 124, 0.13);
  -moz-box-shadow: -1px 4px 16px 7px rgba(118, 121, 124, 0.13);
  box-shadow: -1px 4px 16px 7px rgba(118, 121, 124, 0.13);

  &__username {
    margin: 0;

    font-weight: 500;
    color: $dark-blue
  }

  &__list {
    @include list-zero;
  }

  &>*:not(:last-child) {
    margin-bottom: 12px;
  }
}

.info-list {
  @extend %text-second;

  &>li:not(:last-child) {
    margin-bottom: 4px;
  }
}

.btns-list {
  &>li:not(:last-child) {
    margin-bottom: 12px;
  }

  &>li:last-child {
    padding-top: 12px;
  }

  &__link {
    @include link;

    &:hover {
      color: $dark-blue;
      text-decoration: underline;
    }

    &_logout:hover {
      color: red;
      text-decoration: none;
    }
  }
}
</style>