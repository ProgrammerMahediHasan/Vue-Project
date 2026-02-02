<template>
  <div>
    
<h2>Customer Create</h2>

<h5>{{ customer }}</h5>

<form  @submit.prevent="handleCreate">

<div>
    <label>Name</label>
    <input type="text" name="name" v-model="customer.name">
</div>

<div>
    <label>Email</label>
    <input type="text" name="email" v-model="customer.email">
</div>

<div>
    <label>Phone</label>
    <input type="text" name="phone" v-model="customer.phone">
</div>

<div>
    <label>Address</label>
    <input type="text" name="address" v-model="customer.address">
</div>

<div>
    <button type="submit">Submit</button>
</div>

</form>

  </div>
</template>

<script setup>
import axios from 'axios';
import { useRouter } from 'vue-router';
import { router } from '../../router';
import { reactive } from 'vue';


const baseUrl=import.meta.env.VITE_API_BASE_URL;
const route=useRouter()

 let customer = reactive({
   
  name:"",
  email:"",
  phone:"",
  address:""

 })

function handleCreate()
{
    axios.post(`${baseUrl}/customers`, {customer})
    .then(res=>
{
    console.log(res);
    router.push("/customers")
})
.catch()
}


</script>

<style>

</style>