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
    <div class="abo-content">
      <slot></slot>
    </div>

    <div class="abo-overlay">
      <div class="abo-top clearfix">
        <app-circulartton 
        @click.native="$emit('on-close', false)" 
        bg="#e53935">
          <img src="../../assets/images/x-white.svg" 
            alt="Close button" />
        </app-circulartton>
      </div>

      <div class="abo-bottom">
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

  .abo-content {
    width: inherit;
    height: inherit;
    opacity: none;
    transition-property: opacity;
    transition-duration: .25s;
  }

  .abo-overlay {
    width: inherit;
    height: inherit;
    flex-direction: column;
    position: fixed;
    top: 0;
    display: none;
  }

    .abo-top {
      width: 100%;
      padding: 5px;

      button {
        float: right;
      }
    }

    .abo-bottom {
      width: 100%;
      height: 100%;
      padding: 5px 5px 0 5px;
      position: relative;
      display: flex;
    }
}

.abo-container.show {
  .abo-content {
    opacity: 0.4;
    filter: blur(10px);
  }

  .abo-overlay {
    display: flex;
  }
}
</style>
