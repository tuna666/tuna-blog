<template>
  <section class="dark:bg-gray-800 dark:text-gray-100">
    <div class="container max-w-screen-lg p-6 mx-auto space-y-6 sm:space-y-12">

      <!-- 最初の1個だけ特別な処理 -->
      <NuxtLink v-if="data?.contents && data.contents.length > 0" :to="`/${data.contents[0].id}`" class="block shadow-md rounded-md gap-3 mx-auto sm:max-w-full group hover:no-underline focus:no-underline lg:grid lg:grid-cols-12 dark:bg-gray-900">
        <img :src="data.contents[0].eyecatch?.url" alt="" class="lg:col-span-12 dark:bg-gray-500 rounded-t-md object-cover w-full" :style="{ aspectRatio: 'auto' }">
        <div class="p-6 space-y-2 lg:col-span-12">
          <div class="inline-block rounded border-2 border-indigo-600 px-1.5 py-0.5 text-sm font-semibold text-indigo-600">
            {{ data.contents[0].category?.name }}
          </div>
          <h3 class="text-lg font-semibold sm:text-4xl group-hover:underline group-focus:underline">{{ data.contents[0].title }}</h3>
          <span class="text-xs dark:text-gray-400">{{ dateFormat(data.contents[0].publishedAt ?? data.contents[0].createdAt) }}</span>
          <p>記事概要をここに後ほど挿入。descなどしてapiスキーマを設定？</p>
        </div>
      </NuxtLink>

      <!-- 2個目以降の処理 -->
      <div class="grid justify-center grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <NuxtLink v-for="(blog, index) in data?.contents.slice(1)" :key="blog.id" :to="`/${blog.id}`" class="shadow-md rounded-md max-w-sm mx-auto group hover:no-underline focus:no-underline dark:bg-gray-900">
          <img :src="blog.eyecatch?.url" alt="" class="rounded-t-md dark:bg-gray-500 object-cover w-full" :style="{ aspectRatio: 'auto' }">
          <div class="p-6 space-y-2">
            <div class="inline-block rounded border-2 border-indigo-600 px-1.5 py-0.5 text-sm font-semibold text-indigo-600">
              {{ blog.category?.name }}
            </div>
            <h3 class="font-semibold group-hover:underline group-focus:underline">{{ blog.title }}</h3>
            <span class="text-xs dark:text-gray-400">{{ dateFormat(blog.publishedAt ?? blog.createdAt) }}</span>
            <p>記事概要をここに後ほど挿入。descなどしてapiスキーマを設定？</p>
          </div>
        </NuxtLink>
      </div>

      <!--      <div class="flex justify-center">-->
      <!--        <button type="button" class="px-6 py-3 text-sm rounded-md hover:underline dark:bg-gray-900 dark:text-gray-400">Load more posts...</button>-->
      <!--      </div>-->

    </div>
  </section>
</template>

<script setup lang="ts">
import {Blog} from "~/types/blog";
  const { data } = await useMicroCMSGetList<Blog>({
    endpoint: 'blogs',
  });
console.log(data)
</script>