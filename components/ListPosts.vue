<script setup lang="ts">
import axios from "axios";
import { baseURL } from "@/config/config";

const posts = ref<Array<any>>([]);

onMounted(() => {
  sendGetAllPosts();
});

function sendGetAllPosts() {
  axios
    .get(`${baseURL}/posts`)
    .then((response) => {
      posts.value = response.data;
    })
    .catch(() => {
      console.log("error");
    });
}

function clickPost(post: any) {
  emits("onClickPost", post);
}

const emits = defineEmits(["onClickPost"]);
</script>

<template>
  <div class="bg-white py-8 sm:py-8">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl lg:max-w-4xl">
        <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">
          Blog Dev
        </h2>
        <p class="mt-2 text-lg leading-8 text-gray-600">
          Aprenda programar em vue e nuxt.
        </p>
        <div class="mt-16 space-y-20 lg:mt-20 lg:space-y-20">
          <article
            v-for="post in posts"
            :key="post.id"
            class="relative isolate flex flex-col gap-8 lg:flex-row"
          >
            <div
              class="relative aspect-[16/9] sm:aspect-[2/1] lg:aspect-square lg:w-64 lg:shrink-0"
            >
              <img
                :src="post.imageUrl"
                alt=""
                class="absolute inset-0 h-full w-full rounded-2xl bg-gray-50 object-cover"
              />
              <div
                class="absolute inset-0 rounded-2xl ring-1 ring-inset ring-gray-900/10"
              />
            </div>
            <div @click="clickPost(post)">
              <div class="flex items-center gap-x-4 text-xs">
                <time :datetime="post.datetime" class="text-gray-500">{{
                  post.datetime
                }}</time>
                <a
                  href="#"
                  class="relative z-10 rounded-full bg-gray-50 px-3 py-1.5 font-medium text-gray-600 hover:bg-gray-100"
                  @click.prevent
                  >{{ post.category }}</a
                >
              </div>
              <div class="group relative max-w-xl">
                <h3
                  class="mt-3 text-lg font-semibold leading-6 text-gray-900 group-hover:text-gray-600"
                >
                  <a :href="post.href" @click.prevent>
                    <span class="absolute inset-0" />
                    {{ post.title }}
                  </a>
                </h3>
                <p class="mt-5 text-sm leading-6 text-gray-600">
                  {{ post.description }}
                </p>
              </div>
            </div>
          </article>
        </div>
      </div>
    </div>
  </div>
</template>
