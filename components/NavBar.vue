<script setup>
  const hamburgerActive = ref(false);
</script>

<template>
  <nav class="bg-white dark:bg-gray-900 fixed w-full z-20 top-0 left-0 border-b border-gray-200 dark:border-gray-600">
    <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
      <NuxtLink to="/" @click='hamburgerActive=false' class="flex items-center">
        <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">Tuna Blog</span>
      </NuxtLink>
      <div class="flex md:order-2">
        <div class="hamburger md:hidden" @click='hamburgerActive=!hamburgerActive'>
          <span class="line line01" v-bind:class="{'v-line01':hamburgerActive}"></span>
          <span class="line line02" v-bind:class="{'v-line02':hamburgerActive}"></span>
          <span class="line line03" v-bind:class="{'v-line03':hamburgerActive}"></span>
        </div>
      </div>
      <transition name="menu">
        <div :class="{'hidden': !hamburgerActive}" class="items-center justify-between w-full md:flex md:w-auto md:order-1">
          <ul class="flex flex-col p-4 md:p-0 mt-4 font-medium border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700">
            <li>
              <NuxtLink to="/" @click='hamburgerActive=!hamburgerActive' class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700">Home</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/school" @click='hamburgerActive=!hamburgerActive' class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700">スクール比較</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/ex1" @click='hamburgerActive=!hamburgerActive' class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700">ex1</NuxtLink>
            </li>
          </ul>
        </div>
      </transition>
    </div>
  </nav>
</template>
