<script setup>
import { reactive } from 'vue'

  const estado = reactive({
    filtro: 'todas', //Para filtragem
    tarefaTemp: '',  //Para armazenar e cadastrar
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: true,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: true,
      },
      {
        titulo: 'Ir para a academia',
        finalizada: false,
      }
    ]
  })
//////////////// Sistema de filtragem
  const getTarefasPendentes = () => { 
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }
  const getTarefasFinalizadas = () => { 
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }
  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  //////////////////// Cadastra tarefas
  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = ''; // Para limpar o campo depois de cadastra
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-black rounded-4">
      <h1 class="text-light">Minhas tarefas</h1>
      <p class="text-light">Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastraTarefa"> <!--.prevent - seria o preventDefault -->
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui as tarefas" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
