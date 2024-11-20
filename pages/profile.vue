<script setup lang="ts">
const client = useSupabaseClient()

const user = useSupabaseUser()
const name = ref('')
const loading = ref(true)

if (user.value) {
  const { data } = await client
    .from('profiles')
    .select('name')
    .eq('id', user.value.id)
    .single()
  
  if (data) {
    name.value = data.name
  }
  
}

loading.value = false

async function signOut() {
  try {
    loading.value = true
    if (confirm('Are you sure you want to logout?')) {
      const { error } = await client.auth.signOut()
      if (error) throw error
      user.value = null

      navigateTo('/login')
    } else {
      return null
    }
  } catch (error: any) {
    alert(error.message)
  } finally {
    loading.value = false
  }
}

</script>

<template>
  <div class="w-full">
    <div class="flex flex-col w-[480px] shadow-lg rounded-lg p-6 mx-auto gap-4">
      <div class="flex flex-col gap-1">
        <h1 class="text-2xl font-semibold">
          Hello, {{ loading ? 'loading..' : name }}
        </h1>
        <span class="text-lg">{{ user?.email }}</span>
      </div>

      <button class="min-w-[120px] text-lg bg-blue-500 text-white p-2 rounded-lg" @click="signOut" :disabled="loading">
        Logout
      </button>
    </div>
  </div>
</template>