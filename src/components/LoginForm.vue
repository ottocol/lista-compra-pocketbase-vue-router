<script setup>
    import { reactive } from 'vue'
    import { login } from '@/backend/services/authService';
    import { RouterLink } from 'vue-router';

    let usuario = reactive({email:"", password:""})

    async function doLogin() {
        try {
            await login(usuario.email,usuario.password)
        }
        catch(error) {
            alert("Usuario y/o contraseña incorrectos")
            console.log(error)
        }
    }

</script>

<template>
    <form id="login-form" @submit.prevent="doLogin">
        <h2>Iniciar sesión</h2>
        <label for="email">Correo electrónico:</label>
        <input type="email" name="email" required v-model="usuario.email">
        
        <label for="password">Contraseña:</label>
        <input type="password" name="password" required v-model="usuario.password">
        
        <button type="submit">Iniciar sesión</button>
        <!-- un enlace gestionado por el router -->
        <RouterLink to="/about">
            Acerca de la app
        </RouterLink>  
    </form>
</template>