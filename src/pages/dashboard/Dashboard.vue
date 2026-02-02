

<script setup>
import { ref } from "vue";


let Name="Mahedi Hasan"
let Address= "Narayanganj, Dhaka"
let html="<span>Full Stack Web Developer</span>"

let active=ref (true)
const ChangeName=()=> {
  active.value= !active.value;
}

let customers= ['Abdullah','Harun','Pollob','Rased','Biplod'];

</script>



<template>
  <Counter/>
<h1>Hello! {{Name}}</h1>
<p>Address: {{ Address }}</p>
<h2 v-html="html" style="color:red;"></h2>
<h3 v-if="active" style="background-color:green;color:white;">Mahedi Hasan</h3>
<h4 v-else style="background-color:red;color:black;">Data Not Found</h4>
<button v-on:click="ChangeName" style="background-color:blue;color:white">ChangeName</button>

<ol v-if="active">
  <li v-for="(customer, i) in customers" :key="i">
    {{ customer }}
  </li>
</ol>



</template>



<style scoped>

</style>
