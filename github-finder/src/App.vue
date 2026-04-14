<script setup lang="ts">
import { ref } from "vue"

const username = ref("")
let user = ref(null);

async function buscar() {
  const resposta = await fetch(`https://api.github.com/users/${username.value}`)

  if (!resposta.ok) throw new Error("Não foi possivel")

  const dados = await resposta.json();
}

</script>

<template>
  <main class="h-screen w-screen flex flex-col justify-center items-center gap-4 px-9">
    <section class="flex gap-5 bg-gray-300 justify-center items-center rounded w-full max-w-md shadow-sm" >
    <label for="" class=""></label>
    <input type="text" v-model="username" class="w-full outline-none" placeholder="Digite um nome... ">
    <button class="bg-blue-400 p-2 text-white rounded hover:bg-blue-900 cursor-pointer " @click="buscar()">Buscar</button>
  </section>

  <section class="bg-blue-100 flex justify-center p-4 w-full max-w-md h-50 rounded">
    <p class="">{{user}}</p>
  </section>
  </main>
  


 
</template>
