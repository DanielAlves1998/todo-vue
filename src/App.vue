<script setup>
import { reactive } from 'vue';

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
  <header class="p-5 mb-4 mt-4 bg-light rounded-3"> <!--o rounded ele aredonda as bordas-->
    <h1>Minhas tarefas</h1>
    <p>
      Você possui {{ getTarefasPendentes().length }} tarefas pendentes
    </p>
  </header>
  <form @submit.prevent="cadastraTarefa"> <!--o .prevent é a ,es,a coisa que o preventDefalt que não deixa que a página seja carregada-->
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
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
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"> <!--@change="evento => tarefa.finalizada = evento.target.checked" é uma evento que quando clica ele da um risco em marca com um v de certo-->
      <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo"> <!--MS é margem estatc, dá uma margem borom-->
        {{tarefa.titulo}}
      </label>
    </li>
  </ul>
</div>


</template>

<style scoped>
.done { /*done significa pronto*/
  text-decoration: line-through; /*com isso adiciona um risco*/
}

</style>
