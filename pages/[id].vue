<template>
  <div class="max-w-screen-sm mx-auto md:pt-9">
    <template v-if="data">
      <img
          :src="data.eyecatch?.url"
          :width="data.eyecatch?.width"
          :height="data.eyecatch?.height"
          alt=""
          class="mb-6 w-full"
      />
      <div class="px-6">
        <h1 class="text-3xl font-semibold">
          {{ data.title }}
        </h1>
        <div
            class="mt-4 flex flex-col items-start gap-2 md:flex-row md:items-center md:gap-4"
        >
          <div
              class="rounded border-2 border-indigo-600 px-1.5 py-0.5 text-sm font-semibold text-indigo-600"
          >
            {{ data.category?.name }}
          </div>
          <div class="text-sm text-gray-700">
            {{ dateFormat(data.publishedAt ?? data.createdAt) }}
          </div>
        </div>
        <div v-html="data.content" class="prose mt-6 md:mt-10"></div>

      </div>

      <div class="w-full mx-auto mt-12">
        <div class="p-4 border-t border-b md:border md:rounded">
          <div class="flex py-2">
            <img src="https://randomuser.me/api/portraits/men/97.jpg" class="h-24 w-24 rounded-full mr-2 object-cover"/>
            <div>
              <div class="flex items-center justify-between px-3">
                <p class="font-semibold text-gray-700 text-xl"> Mike Sullivan </p>
                <button class="px-4 py-1 text-gray-100 bg-green-700 flex items-center justify-center rounded">
                  フォロー
                </button>
              </div>
              <p class="text-gray-700 p-3">
                Mike writes about technology
                Yourself required no at thoughts delicate landlord it be. Branched dashwood do is whatever it.
              </p>
            </div>
          </div>
        </div>
      </div>
    </template>

    <!-- 関連記事 -->
    <template v-if="data?.related_blogs.length > 1">
      <div class="pt-6 pb-12 px-4 lg:px-0">
        <p class="mb-6 font-semibold">
          こちらもおすすめ
        </p>
        <div class="grid justify-center grid-cols-1 gap-6 md:grid-cols-2">
          <NuxtLink v-for="blog in data.related_blogs" :key="blog.id" :to="`/${blog.id}`" class="shadow-md rounded-md max-w-sm mx-auto group hover:no-underline focus:no-underline dark:bg-gray-900">
            <img :src="blog.eyecatch?.url" alt="" class="rounded-t-md dark:bg-gray-500 object-cover w-full" :style="{ aspectRatio: 'auto' }">
            <div class="p-6 space-y-2">
              <h3 class="font-semibold group-hover:underline group-focus:underline">{{ blog.title }}</h3>
              <span class="text-xs dark:text-gray-400">{{ dateFormat(blog.publishedAt ?? blog.createdAt) }}</span>
              <p>記事概要をここに後ほど挿入。descなどしてapiスキーマを設定？</p>
            </div>
          </NuxtLink>
        </div>
      </div>
    </template>
  </div>
</template>

<script setup lang="ts">
  import { Blog } from "~/types/blog";

  const { params } = useRoute();

  const { data } = await useMicroCMSGetListDetail<Blog>({
    endpoint: "blogs",
    contentId: Array.isArray(params.id) ? params.id[0] : params.id,
  });
  console.log(data)
</script>