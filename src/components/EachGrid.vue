<script setup lang="ts">
const props = defineProps<{
  value: string
}>()
</script>

<template>
    <button :class="'bg-amber-200 h-20 m-1.5'">
        {{ value }}
    </button>
</template>
