<script setup>
import HomepageView from './views/HomepageView.vue'

const isDesktop = window.innerWidth > 1024
const isTablet = window.innerWidth <= 1024 && window.innerWidth > 748
const fruits = ['kiwi', 'banana', 'tomato']
const fruitsMap = {
  kiwi: 'Super kiwi',
  banana: 'Super banana',
  tomato: 'Super Tomato',
}
</script>

<template>
  <template v-if="isDesktop">
    <HomepageView />
  </template>
  <template v-else-if="isTablet">This is tablet</template>
  <template v-else>
    <div v-show="!isDesktop && !isTablet">this is mobile</div>
  </template>
  <div v-show="!isDesktop && !isTablet">this is mobile</div>
  <div :key="fruit" v-for="(fruit, index) in fruits">{{ index }}: {{ fruit }}</div>
  <div :key="fruit" v-for="(fruit, key) in fruitsMap">{{ key }}: {{ fruit }}</div>
  <div :key="val" v-for="val in 5">{{ val }}</div>
  <div :key="char" v-for="char in 'helllo'">{{ char }}</div>
</template>
