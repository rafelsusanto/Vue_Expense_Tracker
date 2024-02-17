<template>
    <form @submit.prevent="onSubmit" class="flex flex-col items-center justify-center w-80 m-auto mt-8 ">
        <h2 class="text-xl font-bold">Add Transaction</h2>
        <div class="border-t border-neutral-500 w-full my-1"></div>
        <div class="flex justify-between w-full mb-2 mt-2">
            <span>Name: </span>
            <input type="text" v-model="text" class="border border-black px-1" placeholder="Enter name ...">
        </div>
        <div class="flex justify-between w-full mb-2">
            <span>Amount: </span>
            <input type="text" v-model="amount" class="border  border-black px-1" placeholder="Enter amount ...">
        </div>
        <button type="submit" class="bg-lime-500 hover:bg-lime-300 border-rounded px-6 border border-black rounded-lg">Add</button>
    </form>
</template>

<script setup>
import {ref} from 'vue';
import {useToast} from 'vue-toastification';
import { defineEmits } from 'vue';

const toast = useToast();

const text = ref('');
const amount = ref('');

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
    if(!text.value || !amount.value){
        toast.error("Both field need to be filled!");
        return;
    }

    if (isNaN(parseFloat(amount.value))) {
    toast.error("Amount field must be a number.");
    return;
}


    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value)
    };

    emit('transactionSubmitted',transactionData);

    text.value = '';
    amount.value = '';
}
</script>