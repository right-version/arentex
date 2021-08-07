<template lang="pug">
  v-container
    h2 Каталог инвентаря
    v-list
      v-list-item
        nuxt-link(to="/") Главная страница
      v-list-item
        nuxt-link(to="/product/1") Страница продукта
</template>