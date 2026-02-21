<script setup lang="ts">
    import EachGrid from './EachGrid.vue';
    import { ref, computed } from 'vue';

    const remembers = ref<Array<string>>(["", "", "", "", "", "", "", "", ""])
    const isUserO = ref<boolean>(true)

    const winningLines = [
        [0, 1, 2], 
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6], 
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8], 
        [2, 4, 6],
    ]


    const handleClick = (value: number): void => {
        if (remembers.value[value] !== "") return
        if (calculateWinner.value) return
        if (isUserO.value) {
            remembers.value[value] = "O"
        } else {
            remembers.value[value] = "X"
        }
        isUserO.value = !isUserO.value
    }

    const reset = (): void => {
        remembers.value = ["", "", "", "", "", "", "", "", ""]
    }

    const calculateWinner = computed((): string | null => {
        for (const [a, b, c] of winningLines) {
            const val = remembers.value[a]
            if (val && val === remembers.value[b] && val === remembers.value[c]) {
                return val
            }
        }
        const isDraw = remembers.value.every(v => v !== "")
        return isDraw ? "Draw" : null
    })


</script>

<template>
    <h1 class="text-center p-5 text-5xl font-bold text-white"><span class="text-shadow-red-500 text-shadow-lg">Tic</span> <span class="text-shadow-yellow-500 text-shadow-lg">Tac</span> <span class="text-shadow-blue-500 text-shadow-lg">Toe</span></h1>
    <div class="grid grid-cols-3 grid-rows-3 max-w-2xs mx-auto">
        <EachGrid v-for="(_, index) in 9" :key="index" @click="handleClick(index)" :value="remembers[index]"/>
    </div>
    <div class="mx-3 mt-10">
        <div v-if='calculateWinner === "Draw"'>This is a Draw</div>
        <div v-else-if="calculateWinner === null">The turn of: {{ isUserO ? "O" : "X"  }}</div>
        <div v-else>Winner is {{ calculateWinner }} </div>
        <button @click="reset" class="shadow shadow-gray-500 px-4 py-1.5 rounded-lg">Reset</button>
    </div>
</template>