<script lang="ts" setup>
  const products = [
    {
      id: 1,
      image: 'https://images.tokopedia.net/img/cache/300-square/VqbcmM/2022/12/15/9b6b539d-3940-4e62-aeda-faac19549bb2.png',
      title: 'AMD Ryzen 9 7950X Socket AM5 Processor',
      price: 'Rp9.124.000'
    },
    {
      id: 2,
      image: 'https://images.tokopedia.net/img/cache/300-square/product-1/2020/10/5/910865/910865_123a439d-0f08-4ccd-9588-46a2cbbea67d_2048_2048',
      title: 'OontZ Angle Solo Super Portable Bluetooth Speaker - Black',
      price: 'Rp254.000'
    }
  ]
</script>

<template>
  <div class="flex flex-col gap-4">
    <h1 class="text-lg font-semibold">Daftar Barang</h1>

    <ul class="flex flex-row flex-wrap gap-2">
      <li 
        class="p-2 rounded-md w-[150px] h-auto shadow-lg" 
        v-for="(product, index) in products"
        :key="index"
      >
        <div class="flex flex-col gap-1">
          <img 
            :src="product.image" 
            alt="gambar produk"
          />
          <h3 class="text-xs">{{ product.title }}</h3>
          <h3 class="text-xs font-bold">{{ product.price }}</h3>
        </div>
      </li>
    </ul>
  </div>
</template>