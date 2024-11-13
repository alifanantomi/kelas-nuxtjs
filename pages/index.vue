<script lang="ts" setup>
const client = useSupabaseClient()

const { data: products } = await useAsyncData('product', async () => {
  const { data } = await client.from('product').select()

  return data
})
</script>

<template>
  <div class="flex flex-col gap-4">
    <h1 class="text-2xl font-semibold">Daftar Barang</h1>

    <ul class="flex flex-row flex-wrap gap-4">
      <li 
        class="p-2 rounded-md w-[250px] h-auto shadow-lg" 
        v-for="(product, index) in products"
        :key="index"
      >
        <NuxtLink :to="`detail/${product.id}`">
          <div class="flex flex-col gap-1">
            <img 
              :src="product.image" 
              alt="gambar produk"
            />
            <h3 class="text-lg">{{ product.title }}</h3>
            <h3 class="text-lg font-bold">{{ product.price }}</h3>
          </div>
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>