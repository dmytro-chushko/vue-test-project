<template>
  <button class="bg-[#FFA279] rounded-xl py-3 px-10 text-white font-bold">
    <div v-if="$slots.default">Hello default slot</div>
    <slot>Default value</slot>
  </button>
</template>
