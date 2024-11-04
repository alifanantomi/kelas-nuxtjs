<template>
  <header class="flex flex-row justify-between items-center px-6 md:px-12 py-3 bg-slate-500 text-white">
    <div>Logo</div>
    <ul class="flex flex-row items-center gap-4">
      <li>
        <NuxtLink to="/">
          Home
        </NuxtLink>
      </li>
      <li>
        <NuxtLink to="/cart">
          Keranjang
        </NuxtLink>
      </li>
      <li>
        <NuxtLink to="/about">
          About
        </NuxtLink>
      </li>
      <li>
        <NuxtLink to="/profile">
          Profile
        </NuxtLink>
      </li>
    </ul>
  </header>
</template>