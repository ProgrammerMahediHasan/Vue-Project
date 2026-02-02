<template>
  <div>
    
<h4>Customer Info</h4>
<table>

    <thead>
        <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Email</th>
            <th>Phone</th>
            <th>Address</th>
            <th>Action</th>
        </tr>
    </thead>

    <tbody>
        <tr  v-for="customer in customers" :key="customer.id">
            <td>{{ customer.id }}</td>
            <td>{{ customer.name }}</td>
            <td>{{ customer.email }}</td>
            <td>{{ customer.phone }}</td>
            <td>{{ customer.address }}</td>
            <td>
                <!-- <button @click="router.push('/customer/edit/${customer.id}')">Edit</button> -->
                <router-link :to="`/customer/edit/${customer.id}`"> Edit</router-link>
                <!-- "`/customers/edit/`" -->
                <!-- <button>Edit</button> -->
                <button>Delete</button>
            </td>
        </tr>
    </tbody>
</table>
  </div>
</template>

<script  setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';
import { router } from '../../router';

const customers=ref([])

const fetchCustomer=()=>{
    axios.get('http://localhost/larvel_vue_api/public/api/customer')
    .then((res)=>{
        console.log(res.data.customers);
        customers.value=(res.data.customers);
    })
    .catch()
}

onMounted(()=>{
    fetchCustomer();
})

</script>

<style>

</style>