<script setup>
    const props = defineProps(['tarefasPendentes']) // o props é de propriedades
</script>


<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3"> <!--o rounded ele aredonda as bordas-->
        <h1>Minhas tarefas</h1>
        <p>
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>