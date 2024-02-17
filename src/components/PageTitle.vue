<template>
  <div class="flex justify-center align-middle mt-10">
    <h1 class="text-2xl font-bold">{{ msg }}</h1>
  </div>
</template>

<script setup>
/* eslint-disable */
  import { defineProps } from 'vue';
  const props = defineProps({
    msg:{
      type: String,
      required: true,
    }
  });
</script>
