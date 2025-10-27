<script setup>
    import { getItems, addItem, updateComprado } from '@/backend/repositories/listaRepository';
    import { logout } from '@/backend/services/authService'
    import { onMounted, reactive } from 'vue';
    import Item from './Item.vue';
    import AddItemForm from './AddItemForm.vue';

    let estado = reactive({items:[]})
    function doLogout() {
        logout()
    }

    onMounted(async function() {
        estado.items = await getItems()
        console.log(estado.items)
    }) 

    async function doAddItem(nuevoNombre) {
        let nuevoItem = await addItem(nuevoNombre) 
        estado.items.push(nuevoItem)
    }
       
    async function doToggleItem(id) {
        let item = estado.items.find((item) => item.id == id)
        if (item) {
            let nuevoValor = !item.comprado
            await updateComprado(id, nuevoValor)
            item.comprado = nuevoValor
        } 
    }
    
</script>

<template>
    <h2>Lista de la compra</h2>
    <add-item-form @add_item="doAddItem"/>
    <ul>
       <item v-for="i in estado.items" :="i" @toggle_item="doToggleItem"/>
    </ul>
    <button @click="doLogout">Salir</button>
</template>