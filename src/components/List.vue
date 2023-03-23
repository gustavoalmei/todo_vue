<script setup>
  const props = defineProps(['tarefas', 'titulo', 'finalizada']);
</script>
<template>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input
        @change="event => tarefa.finalizada = event.target.checked"
        type="checkbox"
        :checked="tarefa.finalizada"
        :id="tarefa.titulo"
      />
      <label
        :class="{ done: tarefa.finalizada }"
        class="ps-2"
        :for="tarefa.titulo"
      >
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</template>
<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>