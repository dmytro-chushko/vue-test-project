<script setup>
import { reactive, toRaw } from 'vue'
import IButton from '../../IButton/IButton.vue'
import IInput from '../../IInput/IInput.vue'
import FormContainer from '../FormContainer.vue'

const emit = defineEmits(['submit'])
const userData = reactive({
  name: '',
  email: '',
  password: '',
})
</script>

<template>
  <FormContainer
    class="max-w-[500px] w-full bg-white p-10 rounded-2xl"
    @submit.prevent="emit('submit', toRaw(userData))"
  >
    <!-- <IInput class="mb-4" label="Повне ім’я" />
    <IInput class="mb-4" label="Електронна пошта" placeholder="email@gmail.com" />
    <IInput label="Пароль" type="password" @input="(e) => console.log(e.target.value)" /> -->
    <IInput class="mb-4" label="Повне ім’я" v-model="userData.name" />
    <IInput
      class="mb-4"
      label="Електронна пошта"
      placeholder="email@gmail.com"
      v-model="userData.email"
    />
    <IButton class="mt-10 w-full" variant="gradient" type="submit">Створити аккаунт</IButton>
  </FormContainer>
</template>
