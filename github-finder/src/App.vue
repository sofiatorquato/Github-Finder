<script setup lang="ts">
import { ref } from "vue"
import axios from "axios";

const username = ref("")
const user = ref<UserDados | null>(null);

interface UserDados{
  name: string | null,
  bio: string | null,
  avatar_url: string,
  html_url:string
}


async function buscar() {
  try {
    const resposta = await axios.get(`https://api.github.com/users/${username.value}`)
    user.value = resposta.data
    
  }
  catch (error) {
   
  }
}

</script> 

<template>
  <main class="h-screen w-screen flex flex-col justify-center items-center gap-4 px-9">
    <section class="gap-5 bg-gray-300 rounded w-full max-w-md shadow-sm" >
  
    <form @submit.prevent="buscar" class="flex">
    <input type="text" v-model="username" class="w-full outline-none px-4" placeholder="Digite um nome... ">
    <button class="bg-blue-400 p-2 text-white rounded hover:bg-blue-900 cursor-pointer " @click="buscar">Buscar</button>
    </form>
    
  </section>

  <section class="bg-blue-100 flex justify-center p-4 w-full max-w-md h-50 rounded flex flex-col items-center" v-if="user">
    <img class="w-20 rounded-xl" :src="user.avatar_url">
    <h2 class="font-bold">{{ user.name  || "Usuário sem nome"}}</h2>
    

    <span class="italic">{{ user.bio  || "Sem biografia"}}</span>
    <a class="underline text-blue-600" :href="user.html_url" target="blank">Ver perfil completo</a>
  </section>

  </main>
  
 
</template>
