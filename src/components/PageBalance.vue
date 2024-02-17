<template>
    <div class="flex align-middle w-1/2 m-auto mt-8 justify-center">
        <h2 class="text-xl font-bold">Balance: </h2>
        <span class="text-xl ml-4">${{ balance }}</span>
    </div>
</template>

<script setup>
/* eslint-disable */ 
import { defineProps } from 'vue';

const props = defineProps({
    balance: {
        type: Number,
        required: true
    }
});
</script>