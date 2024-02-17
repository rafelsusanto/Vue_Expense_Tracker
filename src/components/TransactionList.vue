<template>
    <div class="flex flex-col items-center justify-center w-80 m-auto mt-8 ">
        <h2 class="text-xl font-bold">History</h2>
        <div class="border-t border-neutral-500 w-full my-1"></div>
        <ul class="w-full">
            <li v-if="transactions.length === 0" class=" my-2 w-full relative group">Empty List</li>
            <li v-else v-for="t in transactions" v-bind:key="t.id" class="border-black border my-2 w-full relative group">
                <button @click="deleteTr(t.id)" class="absolute left-0 transform -translate-x-full opacity-0 group-hover:opacity-100 ease-in-out duration-300 bg-red-400 font-bold text-white p-1">X</button>
                <div class="flex justify-between py-1 border-r-4 border-red-600" :class="t.amount > 0 ? 'plus' : ''">
                    <span class="pl-2">{{ t.text }}</span>
                    <span class="pr-2">${{ t.amount }}</span>
                </div>
            </li>
        </ul>
    </div>
</template>

<script setup>
/* eslint-disable */ 
import { defineProps,defineEmits } from 'vue';

const props = defineProps({
    transactions :{
        type: Array,
        required:true
    }
});

// delete transaction
const emit = defineEmits(['transactionDeleted']);
const deleteTr = (id) =>{
    emit('transactionDeleted',id);
};
</script>

<style scoped>
.plus{
    border-color: rgb(5, 255, 47)!important;
}
</style>