<script setup lang="ts">
const client = useSupabaseClient()

const name = ref('')
const email = ref('')
const password = ref('')

const signUpNewUser = async () => {
  const { data, error } = await client.auth.signUp(
    {
      email: email.value,
      password: password.value,
      options: {
        data: {
          name: name.value
        },
      },
    }
  )

  console.log(data);
  console.log(error);
  
}
</script>

<template>
  <div class="w-full">
    <div class="flex flex-col gap-4 w-[480px] mx-auto p-8  shadow-xl rounded-lg">
      <h1 class="text-2xl font-semibold text-center">Register to NuxtCommerce</h1>

      <div class="flex flex-col gap-2">
        <div class="flex flex-col gap-1">
          <label for="name">Name</label>
          <input 
            name="name" 
            type="text" 
            class="w-full border-2 border-slate-600 p-2 rounded-lg"
            v-model="name"
          >
        </div>

        <div class="flex flex-col gap-1">
          <label for="email">Email</label>
          <input 
            name="email" 
            type="email" 
            class="w-full border-2 border-slate-600 p-2 rounded-lg" 
            v-model="email"
          >
        </div>

        <div class="flex flex-col gap-1">
          <label for="password">Password</label>
          <input 
            name="password" 
            type="password" 
            class="w-full border-2 border-slate-600 p-2 rounded-lg" 
            v-model="password"
          >
        </div>
        
        <button @click="signUpNewUser" class="min-w-[120px] text-lg bg-blue-500 text-white p-2 rounded-lg">
          Register
        </button>

        <div class="text-md text-center mt-2">
          Sudah punya akun? 
          <NuxtLink 
            class="text-blue-500 font-semibold" 
            to="/login"
          >
            Login Sekarang
          </NuxtLink> 
        </div>
      </div>
    </div>
    
  </div>
</template>