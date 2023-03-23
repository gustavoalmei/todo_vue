<script setup>
  const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp']);
</script>
<template>
  <form @submit.prevent="props.cadastraTarefa" class="row">
    <div class="col-md-9">
      <input
        required
        :value="props.tarefaTemp"
        @change="props.editaTarefaTemp"
        class="form-control"
        type="text"
        placeholder="Digite uma tarefa"
      />
    </div>
    <div class="col-md-1">
      <input class="btn btn-primary" type="submit" value="Cadastrar" />
    </div>
    <div class="col-md-2">
      <select
        class="form-select"
        @change="props.trocarFiltro"
      >
        <option value="todas">Todas tarefas</option>
        <option value="pendente">Tarefas Pendentes</option>
        <option value="concluida">Tarefas Concluidas</option>
      </select>
    </div>
  </form>
</template>
