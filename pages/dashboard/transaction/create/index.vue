<script setup>
import { ref, computed, onMounted } from 'vue'

const client = useSupabaseClient()

const products = ref([
  { id: 1, title: 'Laptop', price: 120000 },
  { id: 2, title: 'Keyboard', price: 10000 },
  { id: 3, title: 'Mouse', price: 5000 }
])

// Form reactive variables
const selectedProduct = ref(null)
const quantity = ref(1)
const transactionItems = ref([])

const totalPrice = computed(() => {
  return selectedProduct.value 
    ? selectedProduct.value.price * quantity.value 
    : 0
})

const transactionTotal = computed(() => {
  return transactionItems.value.reduce((total, item) => 
    total + (item.product.price * item.quantity), 0)
})

const addTransactionItem = () => {
  if (selectedProduct.value && quantity.value > 0) {
    transactionItems.value.push({
      product: selectedProduct.value,
      quantity: quantity.value
    })
    
    selectedProduct.value = null
    quantity.value = 1
  }
}

const removeTransactionItem = (index) => {
  transactionItems.value.splice(index, 1)
}

const saveTransaction = () => {
  if (transactionItems.value.length > 0) {
    console.log('Saving transaction:', transactionItems.value)
    alert('Transaction saved successfully!')
    transactionItems.value = []
  } else {
    alert('No items in transaction')
  }
}

onMounted(async () => {
  try {
    const { data } = await client.from('product').select().order('created_at', { ascending: true })

    return products.value = data
  } catch (error) {
    console.error('Failed to fetch products', error)
  }
})
</script>

<template>
  <div class="product-transaction-container p-4">
    <h2 class="text-xl font-bold mb-4">Product Transaction Tracker</h2>
    
    <form @submit.prevent="addTransactionItem" class="mb-4">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div>
          <label class="block mb-2">Select Product</label>
          <select 
            v-model="selectedProduct" 
            class="w-full p-2 border rounded"
            required
          >
            <option value="" disabled>Choose a Product</option>
            <option 
              v-for="product in products" 
              :key="product.id" 
              :value="product"
            >
              {{ product.title }} - Rp{{ product.price }}
            </option>
          </select>
        </div>

        <div>
          <label class="block mb-2">Quantity</label>
          <input 
            type="number" 
            v-model.number="quantity" 
            min="1" 
            class="w-full p-2 border rounded"
            required
          />
        </div>

        <div>
          <label class="block mb-2">Total Price</label>
          <input 
            type="text" 
            :value="totalPrice" 
            class="w-full p-2 border rounded bg-gray-100" 
            readonly
          />
        </div>
      </div>

      <button 
        type="submit" 
        class="mt-4 bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600"
      >
        Add to Transaction
      </button>
    </form>

    <div v-if="transactionItems.length" class="mt-6">
      <h3 class="text-lg font-semibold mb-3">Transaction Items</h3>
      <table class="w-full border">
        <thead>
          <tr class="bg-gray-100">
            <th class="p-2 border">Product</th>
            <th class="p-2 border">Quantity</th>
            <th class="p-2 border">Unit Price</th>
            <th class="p-2 border">Total</th>
            <th class="p-2 border">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr 
            v-for="(item, index) in transactionItems" 
            :key="index" 
            class="text-center"
          >
            <td class="p-2 border">{{ item.product.title }}</td>
            <td class="p-2 border">{{ item.quantity }}</td>
            <td class="p-2 border">Rp{{ item.product.price }}</td>
            <td class="p-2 border">Rp{{ (item.product.price * item.quantity) }}</td>
            <td class="p-2 border">
              <button 
                @click="removeTransactionItem(index)"
                class="text-red-500 hover:text-red-700"
              >
                Remove
              </button>
            </td>
          </tr>
        </tbody>
      </table>

      <div class="mt-4 text-right font-bold">
        Transaction Total: Rp{{ transactionTotal }}
      </div>

      <button 
        @click="saveTransaction" 
        class="mt-4 bg-green-500 text-white px-4 py-2 rounded hover:bg-green-600"
      >
        Save Transaction
      </button>
    </div>
  </div>
</template>