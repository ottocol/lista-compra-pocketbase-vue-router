<script setup>
 import ListaCompra from './components/ListaCompra.vue'
 import LoginForm from './components/LoginForm.vue'
 import { pb } from './backend/config/pb'
 import { ref } from 'vue'
 import {RouterView} from 'vue-router'
 import { useRouter } from 'vue-router'
 
 let hay_usuario = ref(pb.authStore.isValid)
 console.log("Hay usuario: ", hay_usuario.value)
 const router = useRouter()

 pb.authStore.onChange((token, model) => {
    console.log("Cambia el estado de auth!!!", model)
    if (model) {
      hay_usuario.value = true
      router.push('/');
    }
    else {
      hay_usuario.value = false
      router.push('/login');
    }
 })

</script>

<template>
  <router-view/>
</template>

<style>
/* Estilos generales */
body {
    font-family: Arial, sans-serif;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    background-color: white;
}

h1, h2 {
    text-align: center;
    color: #333;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}
</style>
