<template>
    <div class="flex items-center w-screen m-auto mt-8 justify-center">
        <div class="w-80 h-16 flex justify-evenly items-center py-2 border-black border-2">
            <div class="grid">
                <span>INCOME</span>
                <span class="text-lime-500 font-bold">+${{ income }}</span>
            </div>
            <div class="border-l border-black h-12"></div>
            <div class="grid">
                <span>EXPENSE</span>
                <span class="text-red-700 font-bold">-${{ expense*-1 }}</span>
            </div>
        </div>
    </div>
</template>

<script setup>
/* eslint-disable */ 
import { defineProps } from 'vue';

const props = defineProps({
    income: {
        type: Number,
        required: true
    },
    expense: {
        type: Number,
        required: true
    }
});
</script>