<template lang="pug">
.logo.mr-8
  .d-none.d-sm-flex ARENTEX
  transition(name="circle")
    .d-flex.d-sm-none(v-if="!isSearch") ARENTEX
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    isSearch: {
      type: Boolean,
      default: false,
    },
  },
})
</script>

<style scoped>
.logo {
  display: flex;
  align-items: center;
  color: white;
  font-size: 30px;
  line-height: 30px;
  font-weight: 500;
}
</style>