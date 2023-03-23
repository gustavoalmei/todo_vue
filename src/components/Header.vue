<script setup>
  const props = defineProps(['tarefasPendentes']);
</script>
<template>
  <header class="bg-light p-5 mb-4 mt-4 rounded-3">
    <h1>Minhas tarefas</h1>
    <p>Você possui {{ props.tarefasPendentes }} tarefas pendêntes</p>
  </header>
</template>
