<script lang="ts" setup>
const router = useRouter()

const onClickCancel = () => {
  console.log("Pindah ke halaman sebelumnya");

  router.back()
}
</script>

<template>
  <div class="flex flex-col gap-4">
    <h1 class="text-2xl font-semibold">
      Tambah Barang
    </h1>

    <form action="#">
      <div class="flex flex-col gap-2">
        <input
          class="p-2 border-2 border-slate-400 rounded-md" 
          placeholder="Judul barang" 
          type="text"
        >
        
        <textarea
          class="p-2 border-2 border-slate-400 rounded-md" 
          placeholder="Deskripsi barang" 
          type="text"
        ></textarea>

        <div class="flex flex-row gap-2 items-center w-full">
          <input
            class="w-full p-2 border-2 border-slate-400 rounded-md" 
            placeholder="Harga barang" 
            type="number"
          >
          
          <input
            class="w-full p-2 border-2 border-slate-400 rounded-md" 
            placeholder="Stok barang" 
            type="number"
          >
        </div>

        <div class="flex flex-col gap-1">
          <label for="image">Gambar Barang</label>
          <input
            name="image"
            class="p-2 border-2 border-slate-400 rounded-md" 
            placeholder="Gambar barang" 
            type="file"
          >
        </div>

        <div class="flex flex-row gap-2 items-center">
          <button type="button" class="w-fit border-2 border-blue-500 text-blue-500 p-2 rounded-lg px-4" @click="onClickCancel">
            Batal
          </button>
          <button type="button" class="w-fit bg-blue-500 text-white p-2 rounded-lg px-4">
            Simpan Barang
          </button>
        </div>

      </div>
    </form>
  </div>
</template>