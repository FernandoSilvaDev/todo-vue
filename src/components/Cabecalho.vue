<script setup>
    const props = defineProps(['tarefasPendentes']) //Props seria propriedades
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-black rounded-4">
        <h1 class="text-light">Minhas tarefas</h1>
        <p class="text-light">Você possui {{ props.tarefasPendentes }} tarefas pendentes</p>
    </header>
</template>