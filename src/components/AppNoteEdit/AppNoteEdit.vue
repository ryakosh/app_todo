<!--
  Props: {
    value: "Used for v-model, Accepts the text to show in the NoteEdit" -> 
      String
  },
  Events: {
    input: "Used for v-model, Emitted when input event
      triggers on NoteEdit" -> (value: String)
  }
-->

<template>
  <textarea class="ane-container" :value="value"
    @input="$emit('input', $event.target.value)">
  </textarea>
</template>

<script>
export default {
  name: 'AppNoteEdit',
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
.ane-container {
  padding: 15px;
  border: none;
  outline: none;
  border-radius: 5px;
  box-shadow: 0px 1px 2px black;
  transition: box-shadow .25s;
  resize: none;

  &:hover, &:focus {
    box-shadow: 0px 2px 5px;
  }
}
</style>
