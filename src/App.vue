<script setup>
    import {reactive} from 'vue';
    import Header from './components/Header.vue';
    import FormList from './components/Form.vue';
    import List from './components/List.vue';

    let estado = reactive({
        filtro: "todas",
        tarefaTemp: "",
        tarefas: [
        {
            titulo: "Estudar ES6",
            finalizada: false
        },
        {
            titulo:"Estudar JSON",
            finalizada:true
        },
        {
            titulo:"Ir para a academia",
            finalizada:false
        }
        ]
    })

    const getTarefasPendentes = ()=>{
        return estado.tarefas.filter(tarefa => !tarefa.finalizada);
    }

    const getTarefasConcluidas = ()=>{
        return estado.tarefas.filter(tarefa => tarefa.finalizada);
    }

    const selectTarefas = ()=>{
        switch(estado.filtro){
            case "pendente":
                return getTarefasPendentes();
            case "concluida":
                return getTarefasConcluidas();
            default:
                return estado.tarefas;
        }
    }

    const setTarefas = ()=>{
        let novaTarefa = estado.tarefaTemp;
        estado.tarefas.push({
            titulo:novaTarefa,
            finalizada:false
        })
        estado.tarefaTemp = "";
    }
</script>

<template>
    <div class="container">
        <Header :tarefas-pendentes="getTarefasPendentes().length"/>
        <FormList 
            :trocar-filtro="event=> estado.filtro = event.target.value" 
            :tarefa-temp="estado.tarefaTemp" 
            :edita-tarefa-temp="event => estado.tarefaTemp = event.target.value" 
            :cadastra-tarefa="setTarefas"/>
        <List :tarefas="selectTarefas()"/>
    </div>
</template>
