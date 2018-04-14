<!--
  Props: {
    show: "If true, overlay will appear, It's used with v-model" -> Boolean
  },
  Events: {
    on-close: "Emitted when overlay's close button is clicked,
      It's used with `v-model`" -> (false: Boolean)
  },
  Slot: {
    default: "Slot used for storing actual page content",
    overlay: "Slot used for storing overlay's content"
  },
  v-model: "Control visibility of the overlay" -> Boolean
-->

<template>
  <div :class="['abo-container', {show}]">
    <div class="content">
      <slot></slot>
    </div>

    <div class="overlay">
      <div class="top clearfix">
        <app-circulartton 
        @click.native="$emit('on-close', false)" 
        bg="#e53935">
          <img src="../../assets/images/x-white.svg" 
            alt="Close button" />
        </app-circulartton>
      </div>

      <div class="bottom">
        <slot name="overlay"></slot>
      </div>
    </div>
  </div>
</template>

<script>
import AppCirculartton from "../AppCirculartton/AppCirculartton";

export default {
  name: "AppBluryOverlay",
  components: {
    AppCirculartton
  },
  model: {
    prop: "show",
    event: "on-close"
  },
  props: {
    show: {
      type: Boolean,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.abo-container {
  width: 100%;
  height: 100%;

  .content {
    width: inherit;
    height: inherit;
    filter: none;
    opacity: none;
    transition-property: filter, opacity;
    transition-duration: .25s;
  }

  .overlay {
    width: inherit;
    height: inherit;
    flex-direction: column;
    position: fixed;
    top: 0;
    display: none;
  }

    .top {
      width: 100%;
      padding: 5px;

      button {
        float: right;
      }
    }

    .bottom {
      width: 100%;
      height: 100%;
      padding: 5px;
      position: relative;
    }
}

.abo-container.show {
  .content {
    filter: blur(10px);
    opacity: 0.4;
  }

  .overlay {
    display: flex;
  }
}
</style>
