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
    <div class="confirm">
      <div class="top">
        <p><slot></slot></p>
      </div>

      <div class="bottom clearfix">
        <app-circulartton class="btn"
          @click.native="onBtnClick(true)"
          bg="#009688">
            <img src="../../assets/images/tick-white.svg" alt="Confirm button" />
        </app-circulartton>

        <app-circulartton class="btn" 
          @click.native="onBtnClick(false)"
          bg="#f44336">
            <img src="../../assets/images/x-white.svg" alt="Reject button" />
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
    event: 'on-close'
  },
  props: {
    show: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    onBtnClick(isConfirmed) {
      this.$emit('on-settled', isConfirmed);
      this.$emit('on-close', false);
    }
  }
}
</script>

<style scoped lang="scss">
.acb-container {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  z-index: 100;
  display: flex;
  justify-content: center;
  align-items: center;

  .confirm {
    width: 90%;
    height: 40%;
    background-color: white;
    padding: 10px;
    display: flex;
    flex-direction: column;
  }

    .top {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .bottom {
      width: 100%;
    }

      .btn {
        float: right;
        margin-right: 8px;
      }
}
</style>
