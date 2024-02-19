<script setup lang="ts">
import axios from "axios";
import { baseURL } from "@/config/config";

const router = useRouter();
const form = ref<any>({
  category: "",
  imageUrl:
    "https://images.unsplash.com/photo-1496128858413-b36217c2ce36?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=3603&q=80",
});

function sendCreatePosts() {
  form.value.datetime = new Date().toISOString();
  axios
    .post(`${baseURL}/posts`, form.value)
    .then(() => {
      console.log("success");
      router.push("/");
    })
    .catch(() => {
      console.log("error");
    });
}
</script>

<template>
  <div class="mx-auto max-w-2xl lg:max-w-4xl mt-8">
    <div class="font-semibold text-3xl">Novo post</div>

    <div>
      <label
        for="email"
        class="block text-sm font-medium leading-6 text-gray-900"
        >Titulo</label
      >
      <div class="mt-2">
        <input
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="titulo"
          v-model="form.title"
        />
      </div>
    </div>

    <div>
      <label
        for="email"
        class="block text-sm font-medium leading-6 text-gray-900"
        >Categoria</label
      >
      <div class="mt-2">
        <input
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Categoria"
          v-model="form.category"
        />
      </div>
    </div>

    <div>
      <label
        for="email"
        class="block text-sm font-medium leading-6 text-gray-900"
        >URL da imagem</label
      >
      <div class="mt-2">
        <input
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="URL da imagem"
          v-model="form.imageUrl"
        />
      </div>
    </div>

    <div>
      <label class="block text-sm font-medium leading-6 text-gray-900"
        >Descrição</label
      >
      <div class="mt-2">
        <textarea
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Descrição"
          v-model="form.description"
        >
        </textarea>
      </div>
    </div>

    <div>
      <label class="block text-sm font-medium leading-6 text-gray-900"
        >Conteudo</label
      >
      <div class="mt-2">
        <textarea
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Conteudo"
          v-model="form.content"
          rows="15"
        >
        </textarea>
      </div>
    </div>
  </div>
  <div class="flex flex-row-reverse mx-auto max-w-2xl lg:max-w-4xl mt-8 mb-8">
    <button
      type="button"
      class="rounded-md bg-indigo-600 px-2.5 py-1.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      @click="sendCreatePosts"
    >
      Salvar
    </button>
  </div>
</template>

<style></style>
