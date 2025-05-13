<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocarfiltro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
