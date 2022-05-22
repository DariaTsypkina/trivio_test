<template>
  <a href="#" :class="`menu-list__link ${className}`">
    <slot />
  </a>
</template>

<script>
export default {
  props: {
    className: String
  }
};
</script>

<style lang="scss">
@import "src/styles/main.scss";

// animation
@keyframes slide-border {
  0% {
    width: 0%;
  }

  100% {
    width: 100%;
  }
}

.menu-list__link {
  position: relative;
  padding: 8px 0;
  vertical-align: middle;

  white-space: nowrap;
  @include link;

  transition: color .4s;

  &:hover:not(&_logo):not(&_services),
  &_selected {
    color: $blue;
    transition: color .4s;

    &::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 1.5px;
      background-color: $blue;
      animation: slide-border .4s;
    }
  }

  &_services {
    padding: 8px 12px;

    color: $dark-blue;

    background-color: $dark-gray;
    border-radius: 6px;
    transition: background-color .4s;

    &:hover {
      background-color: $gray;
      transition: background-color .4s;
    }
  }
}
</style>