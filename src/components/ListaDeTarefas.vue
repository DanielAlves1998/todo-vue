<script setup>
    const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"> <!--@change="evento => tarefa.finalizada = evento.target.checked" é uma evento que quando clica ele da um risco em marca com um v de certo-->
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo"> <!--MS é margem estatc, dá uma margem borom-->
                {{tarefa.titulo}}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done { /*done significa pronto*/
    text-decoration: line-through; /*com isso adiciona um risco*/
}
</style>