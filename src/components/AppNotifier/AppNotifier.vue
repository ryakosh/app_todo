<!--
  Props: {
    show: "Used to control the visibility of the notifier" -> Boolean
  },
  Slots: {
    default: "Used to place content in the notifier"
  }
-->

<template>
  <div :class="['an-container', {show}]">
    <span><slot></slot></span>
  </div>
</template>

<script>
export default {
  name: 'AppNotifier',
  props: {
    show: {
      required: true,
      type: Boolean,
    },
  },
};
</script>

<style lang="scss" scoped>
$notifier-height: 20px;
$notifier-padding: 20px;

.an-container {
  width: 100%;
  height: $notifier-height;
  padding: $notifier-padding;
  background-color: #212121;
  position: fixed;
  bottom: 0;
  transition: transform .25s;
  transform: translateY($notifier-height + $notifier-padding);
  color: white;
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  will-change: transform;

  &.show {
    transform: translateY(0);
    box-shadow: 0 -1px 12px black;
  }
}
</style>
