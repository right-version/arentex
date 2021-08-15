<template lang="pug">
.search-container
  .search
    input#trigger.search__checkbox(type="checkbox" v-model="value")
    label.search__label-init(for="trigger")
    label.search__label-active(for="trigger")
    .search__border
    input.search__input(type="text" ref="search")
    .search__close

</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      value: false,
    }
  },
  watch: {
    value() {
      const search = this.$refs.search as HTMLInputElement
      if (this.value && search) {
        requestAnimationFrame(() => {
          search.focus()
        })
      }
      this.$emit('change', this.value)
    },
  },
})
</script>

<style lang="scss" scoped>
$cub: cubic-bezier(0.73, 0.14, 0.4, 1.58);
$step1: 0.15s;
$step2: 0.3s;
$delayClose1: 0.15s;
$delayClose2: 0.3s;
$totalAnim: $step1 + $step2;
$w: 100%;
$h: 40px;
$borderW: 3px;

.search-container {
  position: relative;
  width: 100%;
}
.search {
  position: absolute;
  top: 50%;
  right: 0%;
  margin-left: $w/-2;
  margin-top: $h/-2;
  width: $w;
  height: $h;
  max-width: 400px;

  &__border {
    position: absolute;
    top: 50%;
    right: 0%;
    width: $h;
    height: 100%;
    border: $borderW solid #fff;
    border-radius: 100px;
    transform: translate(0, -50%);
    transition: width $step2 $delayClose2;

    #trigger:checked ~ & {
      transition: width $step2 $step1;
      width: 100%;

      &:after {
        width: 0;
        transition: width $step1 cubic-bezier(0.42, -0.7, 0.62, 1.25);
      }
    }

    &:after {
      content: '';
      position: absolute;
      bottom: -31px;
      right: -31px;
      width: 15px;
      height: $borderW;
      background: #fff;
      border-radius: $h/10;
      transform-origin: 100% 50%;
      transform: rotate(225deg) translateX(3rem);
      transition: width $step1 $delayClose2 + $step2;
    }
  }

  &__input {
    position: relative;
    width: calc($w - $h);
    height: $h;
    padding: $h * 0.15 0 $h * 0.15 $h * 0.4;
    background: transparent;
    outline: none;
    border: none;
    font-size: $h * 0.4;
    color: #fff;
    z-index: -1;
    opacity: 0;
    transition: opacity 0.2s;

    #trigger:checked ~ & {
      opacity: 1;
      z-index: auto;
      transition: opacity 0.2s $totalAnim;
    }
  }

  &__checkbox {
    position: absolute;
    top: -9999px;
    left: -9999px;
    opacity: 0;
    z-index: -10;
  }
  &__label-init {
    z-index: 2;
    position: absolute;
    top: 0;
    right: 0;
    width: $h;
    height: $h;
    cursor: pointer;

    #trigger:checked ~ & {
      transform: scale(0);
    }
  }
  &__label-active {
    z-index: 3;
    position: absolute;
    top: $h/4;
    right: $h/4;
    width: $h/2;
    height: $h/2;
    cursor: pointer;
    transform: scale(0);

    #trigger:checked ~ & {
      transition: transform 0 $totalAnim;
      transform: scale(1);
    }
  }

  &__close {
    position: absolute;
    top: $h/4;
    right: $h/4;
    width: $h/2;
    height: $h/2;
    cursor: pointer;
    z-index: -1;

    #trigger:checked ~ & {
      z-index: auto;

      &:before {
        transform: rotate(-45deg);
        opacity: 1;
        transition: transform 0.2s $totalAnim $cub, opacity 0.1s $totalAnim;
      }
      &:after {
        transform: rotate(45deg);
        opacity: 1;
        transition: transform 0.2s ($totalAnim + $delayClose1) $cub,
          opacity 0.1s ($totalAnim + $delayClose1);
      }
    }

    &:before,
    &:after {
      content: '';
      position: absolute;
      top: $h/5;
      left: 0;
      width: 100%;
      height: $borderW;
      background: #fff;
      border-radius: 0.5rem;
      opacity: 0;
    }
    &:before {
      transform: rotate(-45deg) translateX(2rem);
      transition: transform 0.2s, opacity 0.1s 0.1s;
    }
    &:after {
      transform: rotate(45deg) translateX(2rem);
      transition: transform 0.2s 0.2s, opacity 0.1s 0.3s;
    }
  }
}
</style>