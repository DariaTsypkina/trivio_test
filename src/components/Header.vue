<template>
  <div class="header-wrapper">
    <header class="header">
      <nav>
        <ul class="list menu-list">
          <li>
            <menu-button className="menu-list__link_logo">
              <img src="/src/assets/icons/logo.svg" alt="Trivio" />
            </menu-button>
          </li>
          <li v-for="(item, idx) of menu" :key="idx" @click="() => setSelected(item)">
            <menu-button
              :class="`${item === selected && item !== `Пакеты услуг` ? `menu-list__link_selected` : ``} ${item === `Пакеты услуг` ? `menu-list__link_services` : ``}`">
              <img v-if="item === `Пакеты услуг`" src="/src/assets/icons/cart.svg" alt="cart" />
              {{ item }}
            </menu-button>
          </li>
        </ul>
      </nav>

      <ul class="list cabinet-list">
        <li v-for="{ icon, alt } of icons" :key="icon" class="cabinet-list__item">
          <button class="cabinet-list__btn">
            <img :src="`/src/assets/icons/${icon}.svg`" :alt="`${alt}`">
          </button>
          <span v-if="icon === `clock`" class="badge badge_history">3</span>
          <span v-if="icon === `envelope`" class="badge badge_messages">&#8226;</span>
        </li>
        <li class="cabinet-list__item" @click="() => isProfileOpened = !isProfileOpened">
          <button class="cabinet-list__btn cabinet-list__btn_profile">
            {{ shortName }}
          </button>
        </li>

        <Transition name="fade">
          <Profile v-if="isProfileOpened" :username="username" v-click-outside="() => (isProfileOpened = false)" />
        </Transition>

        <li class="cabinet-list__item">
          <button class="cabinet-list__btn cabinet-list__btn_lang"
            @click="() => lang === `ru` ? setLang(`eng`) : setLang(`ru`)">
            <img :src="`/src/assets/icons/${lang}.svg`" :alt="`${lang}`">
          </button>
        </li>
      </ul>
    </header>
  </div>
</template>

<script>
import { ref } from "vue";
import MenuButton from "./MenuButton.vue";
import Profile from "./Profile.vue";

export default {
  components: { MenuButton, Profile },

  data() {
    return {
      menu: ["Рабочий стол", "Поездки", "Оплаты", "Мои документы", "Пакеты услуг"],
      selected: "Рабочий стол",
      icons: [
        {
          icon: "search",
          alt: "Поиск"
        },
        {
          icon: "exclamation",
          alt: "Уведомления"
        },
        {
          icon: "clock",
          alt: "История"
        },
        {
          icon: "heart",
          alt: "Сохранения"
        },
        {
          icon: "envelope",
          alt: "Сообщения"
        }
      ],
      lang: "ru",
      username: "Admin Admin",
      isProfileOpened: ref(false)
    };
  },

  methods: {
    setSelected(value) {
      this.selected = value;
    },
    setLang(value) {
      this.lang = value;
    },
  },

  computed: {
    shortName() {
      const name = this.username.split(" ")[0].toLowerCase();
      const surname = this.username.split(" ")[1].toLowerCase();
      return name.charAt(0) + surname.charAt(0);
    }
  },
};
</script>

<style lang="scss">
@import "src/styles/main.scss";

.header {
  &-wrapper {
    -webkit-box-shadow: 0px 8px 14px 3px rgba(30, 33, 36, 0.1);
    -moz-box-shadow: 0px 8px 14px 3px rgba(30, 33, 36, 0.1);
    box-shadow: 0px 8px 14px 3px rgba(30, 33, 36, 0.1);
  }

  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;

  max-width: 1440px;
  padding: 20px 16px;
  margin: 0 auto;
}

.list {
  display: flex;
  align-items: center;
  gap: 16px;

  @include list-zero;
}

.cabinet-list {
  position: relative;

  &__item {
    position: relative;

    & .badge {
      position: absolute;
      right: 2px;

      &_history {
        top: 2px;

        font-size: .6rem;
        color: $normal-gray;
      }

      &_messages {
        top: -7px;

        font-size: 1.5rem;
        color: $blue;
      }
    }
  }

  &__btn {
    padding: 10px;
    border: none;
    border-radius: 6px;
    background: none;
    transition: background-color .4s;
    cursor: pointer;

    &>img {
      vertical-align: middle;
    }

    &:hover:not(&_profile):not(&_lang) {
      background-color: $dark-gray;
      transition: background-color .4s;

      &>img {
        filter: brightness(0) saturate(100%) invert(7%) sepia(59%) saturate(7474%) hue-rotate(238deg) brightness(60%) contrast(121%);
      }

      &+.badge {
        color: $dark-blue;
      }
    }

    &_profile {
      padding: 6px 8px;

      font-family: "Roboto", sans-serif;
      font-size: 1.25rem;

      background-color: $dark-gray;
      transition: background-color .4s;

      &:hover {
        background-color: $gray;
        transition: background-color .4s;
      }
    }
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>