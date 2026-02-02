<template>
  <div>
    <p>{{ customer }}</p>
    <form @submit.prevent="handleupdate">

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

<div><button type="submit">submit</button></div>

    </form>
  </div>
</template>

<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';


let customerId= useRoute().params.customerId
let customer=ref({})
const baseUrl=import.meta.env.VITE_API_BASE_URL;
const fetchCustomer=()=>{
    axios.get (`${baseUrl}/customer/${customerId}`)


    .then(res=>
        { console.log(res);
          customer.value=res.data.customer;            
        })

    .catch(err=> {
        console.log(err); 
                })
}

onMounted(() => {
    fetchCustomer()
})

let handleUpdate =()=>{

axios.put (`${baseUrl}/customer/${customerId}`,{
    customer:customer.value
})
     .then(res=>
        { console.log(res);
          customer.value=res.data.customer;            
        })

    .catch(err=> {
        console.log(err); 
                })
}

</script>




<style>

</style>