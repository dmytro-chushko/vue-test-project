Original file line numberDiff line numberDiff line change @@ -0,0 +1,12 @@
<script setup>
import FavoritePlace from '../FavoritePlace/FavoritePlace.vue'
import IButton from '../IButton/IButton.vue'
import { ref, reactive } from 'vue'
import IInput from '../IInput/IInput.vue'

const counter = ref(0) // { value: 0 }
const user = ref({ name: 'Tom', age: 14 })
const superUser = reactive({ name: 'Super user', age: 1000 })
const { name, age } = superUser
const buttonVariant = ref('gradient')

const props = defineProps({
  items: {
    required: true,
    type: Array,
  },
  activeId: {
    required: true,
    type: [Number, null],
  },
})

const emit = defineEmits(['place-clicked'])

const increment = () => {
  counter.value += 1
}

const changeUserName = () => {
  user.value.name = 'Harry Potter'
}

const changeSuperUserName = () => {
  superUser.name = 'New super user'
}

const changeButtonVariant = () => {
  buttonVariant.value = buttonVariant.value === 'gradient' ? 'outlined' : 'gradient'
}
</script>

<template>
  <div class="px-6">
    <!-- <div class="text-gray">User name: {{ user.name }}</div>
    <div class="text-gray">Super User name: {{ name }}</div> -->
    <div class="text-gray mb-4">Додані маркери ({{ counter }})</div>
    <!-- <div class="text-gray mb-4" @click.stop="() => console.log('click2')">Додані маркери</div> -->
    <div class="py-5">
      <!-- <IInput label="Some label" />
      <a href="/" class="text-black" @click.prevent="() => console.log('prevented')">CLick me</a> -->
    </div>
    <slot name="label"></slot>
    <slot name="list">
      <FavoritePlace
        v-for="place in props.items"
        :key="place.id"
        :title="place.title"
        :description="place.description"
        :img="place.img"
        :is-active="place.id === props.activeId"
        @click="emit('place-clicked', place.id)"
      />
    </slot>

    <slot></slot>
    <IButton class="w-full mt-10" variant="gradient">Додати маркер</IButton>
    <!-- <IButton class="w-full" @click="changeUserName">Change name</IButton>
    <IButton class="w-full mt-2" @click="changeSuperUserName">Change super name</IButton>
    <IButton class="w-full mt-10" @click="increment">Додати маркер</IButton>
    <IButton class="w-full mt-10" variant="gradient" @click="changeButtonVariant"
      >Додати маркер</IButton
    > -->
  </div>
</template>
