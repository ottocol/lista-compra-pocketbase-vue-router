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
    <form @submit.prevent="doLogin">
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

<style scoped>

form {
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

form h2 {
    margin-top: 0;
    margin-bottom: 20px;
}

form label {
    display: block;
    margin-bottom: 5px;
    color: #333;
}

form button {
    width: 100%;
    margin-top: 10px;
}

input[type="text"],
input[type="password"],
input[type="email"] {
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-bottom: 10px;
}

</style>