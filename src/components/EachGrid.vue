<script setup lang="ts">
const props = defineProps<{
  value: string;
  isGameEnd: boolean;
}>()
</script>

<template>
    <button 
        class="h-20 m-1.5 text-2xl"
        :class="value ? (
            value === 'X' ? 'bg-blue-200 text-red-500 text-shadow-lg text-shadow-blue-500' 
                : 'bg-red-200 text-blue-500 text-shadow-lg text-shadow-red-500') 
                : `bg-amber-500 ${!isGameEnd && 'hover:bg-amber-400 cursor-pointer'}`"
    >
        {{ value }}
    </button>
</template>
