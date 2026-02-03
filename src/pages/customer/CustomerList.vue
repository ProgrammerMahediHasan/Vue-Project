<template>
  <div class="customer-container">
    <div class="header-section">
      <h2 class="page-title">Customer List</h2>
      <div class="search-wrapper">
        <input 
          type="text" 
          placeholder="Search customers..." 
          v-model="search"
          class="search-input"
        >
      </div>
    </div>

    <div class="table-wrapper">
      <table class="customer-table">
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Email</th>
                <th>Phone</th>
                <th>Address</th>
                <th>Actions</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="customer in searchCustomer" :key="customer.id">
                <td><span class="id-badge">#{{ customer.id }}</span></td>
                <td class="font-medium">{{ customer.name }}</td>
                <td>{{ customer.email }}</td>
                <td>{{ customer.phone }}</td>
                <td>{{ customer.address }}</td>
                <td class="actions">
                    <router-link :to="`/customer/edit/${customer.id}`" class="btn btn-edit">
                      Edit
                    </router-link>
                    <button class="btn btn-delete">Delete</button>
                </td>
            </tr>
            <tr v-if="searchCustomer.length === 0">
                <td colspan="6" class="empty-state">No customers found</td>
            </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { computed, onMounted, ref } from 'vue';
import { router } from '../../router';

const customers = ref([])

let search = ref("");

const searchCustomer = computed(() => {
    let q = search.value.toLowerCase();
    if (!q) return customers.value;
    return customers.value.filter(customer => {
        return customer.name.toLowerCase().includes(q) || customer.email.toLowerCase().includes(q)
    })
});

const fetchCustomer = () => {
    axios.get('http://localhost/larvel_vue_api/public/api/customer')
        .then((res) => {
            console.log(res.data.customers);
            customers.value = (res.data.customers);
        })
        .catch()
}

onMounted(() => {
    fetchCustomer();
})

</script>

<style scoped>
.customer-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.header-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  flex-wrap: wrap;
  gap: 1rem;
}

.page-title {
  font-size: 1.8rem;
  color: #2c3e50;
  margin: 0;
  font-weight: 600;
}

.search-input {
  padding: 0.75rem 1rem;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  width: 300px;
  font-size: 0.95rem;
  transition: all 0.3s ease;
  outline: none;
  background-color: #fff;
}

.search-input:focus {
  border-color: #646cff;
  box-shadow: 0 0 0 3px rgba(100, 108, 255, 0.1);
}

.table-wrapper {
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  overflow: hidden;
  border: 1px solid #e2e8f0;
}

.customer-table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

.customer-table th {
  background-color: #f8fafc;
  padding: 1rem 1.5rem;
  font-weight: 600;
  color: #475569;
  text-transform: uppercase;
  font-size: 0.75rem;
  letter-spacing: 0.05em;
  border-bottom: 1px solid #e2e8f0;
}

.customer-table td {
  padding: 1rem 1.5rem;
  border-bottom: 1px solid #f1f5f9;
  color: #334155;
  font-size: 0.95rem;
}

.customer-table tr:last-child td {
  border-bottom: none;
}

.customer-table tr:hover {
  background-color: #f8fafc;
}

.font-medium {
  font-weight: 500;
  color: #1e293b;
}

.id-badge {
  background-color: #eff6ff;
  color: #3b82f6;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  font-size: 0.85rem;
  font-weight: 500;
}

.actions {
  display: flex;
  gap: 0.5rem;
}

.btn {
  padding: 0.5rem 1rem;
  border-radius: 6px;
  font-size: 0.875rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  text-decoration: none;
  border: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-edit {
  background-color: #3b82f6;
  color: white;
}

.btn-edit:hover {
  background-color: #2563eb;
}

.btn-delete {
  background-color: #ef4444;
  color: white;
}

.btn-delete:hover {
  background-color: #dc2626;
}

.empty-state {
  text-align: center;
  padding: 3rem;
  color: #94a3b8;
  font-style: italic;
}

/* Dark mode support */
@media (prefers-color-scheme: dark) {
  .page-title {
    color: #f1f5f9;
  }
  
  .customer-container {
    color: #f1f5f9;
  }

  .table-wrapper {
    background-color: #1e293b;
    border-color: #334155;
  }

  .customer-table th {
    background-color: #0f172a;
    color: #94a3b8;
    border-color: #334155;
  }

  .customer-table td {
    border-color: #334155;
    color: #e2e8f0;
  }

  .customer-table tr:hover {
    background-color: #334155;
  }

  .search-input {
    background-color: #1e293b;
    border-color: #334155;
    color: white;
  }

  .font-medium {
    color: #f8fafc;
  }

  .id-badge {
    background-color: #1e3a8a;
    color: #bfdbfe;
  }
}
</style>