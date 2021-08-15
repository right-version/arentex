<template lang="pug">
  .header
    header
      v-container.d-flex.justify-space-between
        .d-flex
          UIBurgerButton.mr-8(v-model="isMenu")
          HeaderLogo(:isSearch="isSearch")
        .d-flex.flex-grow-1
          UISearch(@change="isSearch = $event")
          HeaderProfile.ml-6

    transition(name="circle")
      .header__menu(v-show="isMenu")
        .header__height
        v-container
          HeaderMenu
    .header__height
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      isMenu: false,
      isSearch: false,
    }
  },
})
</script>

<style lang="scss">
.header {
  .header__height {
    height: 64px;
  }

  header {
    position: fixed;
    background-color: $primary;
    height: 64px;
    width: 100%;
    z-index: 1000;
  }

  .header__menu {
    position: fixed;
    background-color: $primary;
    height: 100vh;
    width: 100vw;
    z-index: 999;
  }
}
</style>