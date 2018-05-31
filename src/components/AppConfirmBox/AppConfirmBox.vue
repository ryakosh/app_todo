<!--
  Props: {
    show: "If true, confirm box will appear, It's used with v-model" -> Boolean
  },
  Events: {
    on-close: "Emitted when one of the confirm or reject buttons gets
      clicked, It's used with `v-model`" -> (false: Boolean),
    on-settled: "Emitted when one of the confirm or reject buttons gets
      clicked, `true` means confirmed and `false` means rejected" -> (Boolean)
  },
  Slots: {
    default: "Slot used for storing confirm box text"
  },
  v-model: "Control visibility of the confirm box" -> Boolean
-->

<template>
  <div class="acb-container" v-if="show">
    <div class="acb-confirm">
      <div class="acb-top">
        <p><slot></slot></p>
      </div>

      <div class="acb-bottom clearfix">
        <app-circulartton class="acb-btn"
          @click.native="onBtnClick(true)"
          bg="white">
            <img src="../../assets/images/tick-dark.svg" alt="Confirm button" />
        </app-circulartton>

        <app-circulartton class="acb-btn"
          @click.native="onBtnClick(false)"
          bg="white">
            <img src="../../assets/images/x-dark.svg" alt="Reject button" />
        </app-circulartton>
      </div>
    </div>
  </div>
</template>

<script>
import AppCirculartton from '../AppCirculartton/AppCirculartton';

export default {
  name: 'AppConfirmBox',
  components: { AppCirculartton },
  model: {
    prop: 'show',
    event: 'on-close',
  },
  props: {
    show: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    onBtnClick(isConfirmed) {
      this.$emit('on-settled', isConfirmed);
      this.$emit('on-close', false);
    },
  },
};
</script>

<style scoped lang="scss">
.acb-container {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  display: flex;
  justify-content: center;
  align-items: center;

  .acb-confirm {
    width: 90%;
    height: 40%;
    background-color: #212121;
    padding: 10px;
    display: flex;
    flex-direction: column;
    color: white;
  }

    .acb-top {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .acb-bottom {
      width: 100%;
    }

      .acb-btn {
        float: right;
        margin-right: 8px;
      }
}
</style>
