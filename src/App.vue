<script setup>
  import { reactive } from 'vue';
  import cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'estudar ES6',
      finalizado: false,
    },
    {
      titulo: 'estudar sass',
      finalizado: false,
    },
    {
      titulo: 'Ir para a academia',
      finalizada: true,
    }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefas => !tarefas.finalizada )
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefas => tarefas.finalizada )
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) { //o switch faz varios itens, nesse caso seria "caso todos os filtros... o switch da essa condição de CASO..."
  case 'pendentes':
      return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
        default: //é para quando for um valor diferente desses dois de cima ai ele entra em ação
          return estado.tarefas;
        
  }
}

const cadastraTarefa = () => {
const tarefaNova = {
  titulo: estado.tarefaTemp,
  finalizada: false,
}
estado.tarefas.push(tarefaNova); //o push é para adicionar
estado.tarefaTemp = '';
}

</script>

<template>
<div class="container">
  <cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
  <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
  <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
</div>
</template>
