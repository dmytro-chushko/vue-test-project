<script setup>
import { ref } from 'vue'
import HomepageView from './views/HomepageView.vue'
import FavoritePlace from './components/FavoritePlace/FavoritePlace.vue'
import FavoritePlaces from './components/FavoritePlaces/FavoritePlaces.vue'
import RegistrationForm from './components/Auth/RegistrationForm/RegistrationForm.vue'
import LoginForm from './components/Auth/LoginForm/LoginForm.vue'
import CreateNewPlaceModal from './components/CreateNewPlaceModal/CreateNewPlaceModal.vue'
import { MapboxMap, MapboxMarker } from '@studiometa/vue-mapbox-gl'
import 'mapbox-gl/dist/mapbox-gl.css'
import MarkerIcon from './components/icons/MarkerIcon.vue'

const isOpen = ref(true)
const closeModal = () => {
  isOpen.value = false
}
const openModal = () => {
  isOpen.value = true
}

const mapboxToken = import.meta.env.VITE_MAPBOX_TOKEN
const mapboxStyle = 'mapbox://styles/mapbox/streets-v12'

const isDesktop = window.innerWidth > 1024
const isTablet = window.innerWidth <= 1024 && window.innerWidth > 748
const fruits = ['kiwi', 'banana', 'tomato']
const fruitsMap = {
  kiwi: 'Super kiwi',
  banana: 'Super banana',
  tomato: 'Super Tomato',
}

const favoritePlaces = [
  {
    id: 1,
    title: 'New place 1',
    description: 'SUper description 1',
    img: '',
    lngLat: [30.523333, 50.490001],
  },
  {
    id: 2,
    title: 'New place 2',
    description: 'SUper description 2',
    img: '',
    lngLat: [30.523333, 50.450001],
  },
]

const activeId = ref(null)
const map = ref(null)

const changeActiveId = (id) => {
  activeId.value = id
}

const changePlace = (id) => {
  const { lngLat } = favoritePlaces.find((place) => place.id === id)
  changeActiveId(id)
  map.value.flyTo({ center: lngLat })
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
  <!-- <button @click="openModal">Click me</button>
  <LoginForm @submit="console.log" />
  <RegistrationForm @submit="console.log" />
  <IModal /> 
  <CreateNewPlaceModal :is-open="isOpen" @close="closeModal" @submit="console.log" /> -->

  <!-- WITH MAPBOX -->

  <main class="flex h-screen">
    <div class="bg-white h-full w-[400px] shrink-0 overflow-auto pb-10">
      <FavoritePlaces :items="favoritePlaces" :active-id="activeId" @place-clicked="changePlace" />
    </div>
    <div class="w-full h-full flex items-center justify-center text-6xl">
      <MapboxMap
        class="w-full h-full"
        :center="[30.523333, 50.450001]"
        :zoom="10"
        :access-token="mapboxToken"
        :map-style="mapboxStyle"
        @mb-created="(mapInstance) => (map = mapInstance)"
      >
        <MapboxMarker v-for="place in favoritePlaces" :key="place.id" :lngLat="place.lngLat">
          <button @click="changeActiveId(place.id)">
            <MarkerIcon class="h-8 w-8" />
          </button>
        </MapboxMarker>
      </MapboxMap>
    </div>
  </main>
</template>
