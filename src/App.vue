<script setup>
import HomepageView from './views/HomepageView.vue'
import FavoritePlace from './components/FavoritePlace/FavoritePlace.vue'
import FavoritePlaces from './components/FavoritePlaces/FavoritePlaces.vue'
import RegistrationForm from './components/Auth/RegistrationForm/RegistrationForm.vue'

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
  <!-- <template v-if="isDesktop">
    <HomepageView />
  </template> -->
  <!-- <template v-else-if="isTablet">This is tablet</template>
  <template v-else>
    <div v-show="!isDesktop && !isTablet">this is mobile</div>
  </template>
  <div v-show="!isDesktop && !isTablet">this is mobile</div>
  <div :key="fruit" v-for="(fruit, index) in fruits">{{ index }}: {{ fruit }}</div>
  <div :key="fruit" v-for="(fruit, key) in fruitsMap">{{ key }}: {{ fruit }}</div>
  <div :key="val" v-for="val in 5">{{ val }}</div>
  <div :key="char" v-for="char in 'helllo'">{{ char }}</div> -->
  <!-- <div class="bg-white h-screen w-[400px]">
    <FavoritePlaces>
      <div>THis is super slot</div>
      <template v-slot:label>This is label</template>
      <template #list>This is list</template>
    </FavoritePlaces>
    <FavoritePlaces />
  </div> -->
  <RegistrationForm @submit="console.log" />
</template>
