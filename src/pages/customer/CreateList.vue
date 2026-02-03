<template>
  <div class="form-container">
    <div class="form-card">
      <div class="form-header">
        <h2 class="form-title">Create New Customer</h2>
        <p class="form-subtitle">Enter customer details below</p>
      </div>

      <!-- Debug info hidden or styled nicely if needed -->
      <!-- <h5 class="debug-info">{{ customer }}</h5> -->

      <form @submit.prevent="handleCreate" class="customer-form">
        <div class="form-group">
            <label for="name">Full Name</label>
            <input 
              id="name"
              type="text" 
              name="name" 
              v-model="customer.name" 
              placeholder="e.g. John Doe"
              required
            >
        </div>

        <div class="form-group">
            <label for="email">Email Address</label>
            <input 
              id="email"
              type="email" 
              name="email" 
              v-model="customer.email" 
              placeholder="e.g. john@example.com"
              required
            >
        </div>

        <div class="form-group">
            <label for="phone">Phone Number</label>
            <input 
              id="phone"
              type="tel" 
              name="phone" 
              v-model="customer.phone" 
              placeholder="e.g. +1 234 567 8900"
              required
            >
        </div>

        <div class="form-group">
            <label for="address">Address</label>
            <input 
              id="address"
              type="text" 
              name="address" 
              v-model="customer.address" 
              placeholder="e.g. 123 Main St, City"
              required
            >
        </div>

        <div class="form-actions">
            <button type="button" @click="router.push('/customer')" class="btn-cancel">Cancel</button>
            <button type="submit" class="btn-submit">Create Customer</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { useRouter } from 'vue-router';
import { reactive } from 'vue';


const baseUrl=import.meta.env.VITE_API_BASE_URL;
const router=useRouter()

 let customer = reactive({
   
  name:"",
  email:"",
  phone:"",
  address:""

 })

function handleCreate()
{
    axios.post(`${baseUrl}/customer`, {customer})
    .then(res=>
{
    console.log(res.data.customer);
    router.push("/customer")
})
.catch()
}


</script>

<style scoped>
.form-container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 0 1rem;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.form-card {
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  padding: 2.5rem;
  border: 1px solid #e2e8f0;
}

.form-header {
  margin-bottom: 2rem;
  text-align: center;
}

.form-title {
  font-size: 1.75rem;
  color: #1e293b;
  margin: 0 0 0.5rem 0;
  font-weight: 700;
}

.form-subtitle {
  color: #64748b;
  margin: 0;
  font-size: 0.95rem;
}

.customer-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  text-align: left;
}

.form-group label {
  font-size: 0.9rem;
  font-weight: 600;
  color: #334155;
}

.form-group input {
  padding: 0.75rem 1rem;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-size: 1rem;
  transition: all 0.2s ease;
  background-color: #f8fafc;
}

.form-group input:focus {
  outline: none;
  border-color: #3b82f6;
  background-color: #fff;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.form-actions {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.btn-submit, .btn-cancel {
  flex: 1;
  padding: 0.875rem;
  border-radius: 8px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.2s;
  border: none;
}

.btn-submit {
  background-color: #3b82f6;
  color: white;
}

.btn-submit:hover {
  background-color: #2563eb;
}

.btn-cancel {
  background-color: #f1f5f9;
  color: #475569;
}

.btn-cancel:hover {
  background-color: #e2e8f0;
}

/* Dark mode support */
@media (prefers-color-scheme: dark) {
  .form-card {
    background-color: #1e293b;
    border-color: #334155;
  }

  .form-title {
    color: #f1f5f9;
  }

  .form-subtitle {
    color: #94a3b8;
  }

  .form-group label {
    color: #e2e8f0;
  }

  .form-group input {
    background-color: #0f172a;
    border-color: #334155;
    color: white;
  }

  .form-group input:focus {
    border-color: #60a5fa;
  }

  .btn-cancel {
    background-color: #334155;
    color: #cbd5e1;
  }

  .btn-cancel:hover {
    background-color: #475569;
  }
}
</style>