<script setup>
    defineProps(['id', 'nombre', 'comprado'])
    defineEmits(["toggle_item"])
</script>


<template>
    <li :class="{tachado:comprado}" @click="$emit('toggle_item', id)">{{ nombre }}</li>
</template>

<style scoped>

</style>