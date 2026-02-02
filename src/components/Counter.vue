<template>
   <div style="display:flex; align-items:center; gap:10px;">
    <button 
        @click="descrease"
        style="background-color:red;color:white;font-size:24px;padding:10px 18px;border:none;border-radius:6px;">
        -
    </button>

    <p style="font-size:22px; font-weight:bold;">{{ count }}</p>

    <button 
        @click="increase"
        style="background-color:green;color:white;font-size:24px;padding:10px 18px;border:none;border-radius:6px;">
        +
    </button>
</div>

</template>

<script setup>

import {ref} from 'vue';

let count = ref(0)

function increase() {
    count.value +=1;
}
function descrease(){
    count.value -=1;
}
</script>

<style>
</style>