<!--
  Props: {
    value: "Used for v-model, Accepts the text to show in the EditText" -> 
      String
  },
  Events: {
    input: "Used for v-model, Emitted when input event
      triggers on EditText" -> (value: String)
  }
-->

<template>
  <input class="ate-container" type="text" :value="value"
    @input="$emit('input', $event.target.value)" />
</template>

<script>
export default {
  name: 'AppTextEdit',
  props: {
    value: {
      type: String,
      required: false,
      default: ''
    }
  }
}
</script>

<style lang="scss" scoped>
.ate-container {
  padding: 15px;
  border: 0;
  outline: 0;
  border-radius: 5px;
  box-shadow: 0px 1px 2px black;
  transition: box-shadow .25s;

  &:hover, &:focus {
    box-shadow: 0px 2px 5px;
  }

  &::-webkit-search-decoration,
  &::-webkit-search-cancel-button,
  &::-webkit-search-results-button,
  &::-webkit-search-results-decoration
  { display: none; }

}
</style>
