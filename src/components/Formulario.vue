<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarfiltro', 'editaTarefaTemp'])
</script>
<template>
    <form @submit.prevent="props.cadastraTarefa"> <!--.prevent - atalho do preventDefault de evitar atualizar a pagina-->
      <div class="row">
        <div class="col">
          <!-- :value="estado.tarefaTemp - Para limpar o campo depois de cadastrar" -->
          <!-- @change="evento => estado.tarefaTemp = evento.target.value - Para introduzir novas tarefas -->
          <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui as tarefas" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="props.trocarfiltro" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
</template>