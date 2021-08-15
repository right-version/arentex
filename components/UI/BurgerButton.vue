<template lang="pug">
  label(for="burger")
    input#burger(
      :checked="value"
      @change="$emit('input', $event.target.checked)"
      type="checkbox")
    span
    span
    span

</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    value: {
      type: Boolean,
      default: false,
    },
  },
})
</script>

<style lang="scss" scoped>
label {
  display: flex;
  flex-direction: column;
  width: 40px;
  cursor: pointer;
}

label span {
  background: #fff;
  border-radius: 5px;
  height: 4px;
  margin: 4px 0;
  transition: 0.4s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

span:nth-of-type(1) {
  width: 50%;
}

span:nth-of-type(2) {
  width: 100%;
}

span:nth-of-type(3) {
  width: 75%;
}

input[type='checkbox'] {
  display: none;
}

input[type='checkbox']:checked ~ span:nth-of-type(1) {
  transform-origin: bottom;
  transform: rotatez(45deg) translate(5px, 0px);
}

input[type='checkbox']:checked ~ span:nth-of-type(2) {
  transform-origin: top;
  transform: rotatez(-45deg);
}

input[type='checkbox']:checked ~ span:nth-of-type(3) {
  transform-origin: bottom;
  width: 50%;
  transform: translate(18px, -6px) rotatez(45deg);
}
</style>