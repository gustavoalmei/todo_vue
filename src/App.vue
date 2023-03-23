<script setup>
import {reactive} from 'vue';

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
        <header class="bg-light p-5 mb-4 mt-4 rounded-3">
            <h1>Minhas tarefas</h1>
            <p>
                Você possui {{ getTarefasPendentes().length }} tarefas pendêntes
            </p>
        </header>
        <form @submit.prevent="setTarefas()" class="row">
            <div class="col-md-9">
                <input required :value="estado.tarefaTemp" @change="event => estado.tarefaTemp = event.target.value" class="form-control" type="text" placeholder="Digite uma tarefa">
            </div>
            <div class="col-md-1">
                <input class="btn btn-primary" type="submit" value="Cadastrar">
            </div>
            <div class="col-md-2">
                <select class="form-select" @change="event => estado.filtro = event.target.value">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendente">Tarefas Pendentes</option>
                    <option value="concluida">Tarefas Concluidas</option>
                </select>
            </div>
        </form>
        <ul class="list-group mt-4">
            <li class="list-group-item" v-for="tarefa in selectTarefas()">
                <input @change="event => tarefa.finalizada = event.target.checked" type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
                <label :class="{done: tarefa.finalizada}" class="ps-2" :for="tarefa.titulo">
                    {{ tarefa.titulo }}
                </label>
            </li>
        </ul>
    </div>
</template>

<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>