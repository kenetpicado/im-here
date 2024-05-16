<template>
  <div
    class="flex items-center border border-gray-300 rounded-3xl text-gray-700 overflow-hidden bg-white px-2 py-3 mb-8"
  >
    <input
      type="number"
      required
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      placeholder="Número de cliente"
      class="px-4 w-full focus:outline-none"
    />
    <button
      type="submit"
      aria-label="Buscar"
      class="flex p-2 items-center justify-center bg-danger text-white h-full rounded-full transition select-none duration-300 transform active:scale-110"
    >
      <SearchSvg />
    </button>
  </div>
</template>

<script setup>
import SearchSvg from '@/components/icons/SearchSvg.vue'

defineProps({
  modelValue: {
    type: [String, Number],
    required: false
  }
})
</script>
