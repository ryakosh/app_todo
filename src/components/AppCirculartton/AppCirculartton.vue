<!--
  Props: {
    bg: "Used to change button's background color" -> String,
    fill: "If true, button's <img /> will be 100% of it's container" -> Boolean,
    dark: "If true, <span>'s color will be white" -> Boolean
  },
  Events: {
    click: "<button>'s default `click` event" -> (event: Event)
  },
  Slot: {
    default: "A <span> for text or an <img /> for image"
  }
-->

<template>
<button :class="['ac-btn', {fill, dark}]" type="button"
  :style="`background: ${bg}`" @click="$emit('click')">
  <div class="ac-btn-container">
    <slot></slot>
  </div>
</button>
</template>

<script>
export default {
  name: 'AppCirculartton',
  props: {
    bg: {
      type: String,
      required: false,
      default: 'white',
    },
    fill: {
      type: Boolean,
      required: false,
      default: false,
    },
    dark: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
};
</script>

<style scoped lang="scss">
.ac-btn {
  width: 47px;
  height: 47px;
  border: none;
  border-radius: 50%;
  outline: none;
  cursor: pointer;
  transition-property: width, height;
  transition-duration: .25s;

  &-container {
    width: 100%;
    height: 100%;
    border-radius: inherit;
    display: flex;
    justify-content: center;
    align-items: center;

    span {
      font-size: 16px;
      color: black;
    }
    img {
      width: 16px;
      height: 16px;
    }
  }

  &.dark {
    span {
      color: white;
    }
  }

  &.fill {
    img {
      width: 100%;
      height: 100%;
      border-radius: inherit;
    }
  }
}

@media screen and (min-width: 600px) {
  .ac-btn {
    width: 50px;
    height: 50px;

    &-container {
      img {
        width: 20px;
        height: 20px;
      }
    }
  }
}

@media screen and (min-width: 960px) {
  .ac-btn {
    width: 60px;
    height: 60px;

    &-container {
      img {
        width: 25px;
        height: 25px;
      }
    }
  }
}
</style>
