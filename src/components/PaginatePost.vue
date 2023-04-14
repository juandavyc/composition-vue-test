<script setup>


defineProps({
    inicio: Number,
    fin: Number,
    total: Number,
});

const emit = defineEmits({
    prevPaginacion: Function,
    nextPaginacion: Function
});

const anterior = () => {
    emit('prevPaginacion');
}

const siguiente = () => {
    emit('nextPaginacion');
}




</script>
<template>
    <div class="btn-group gap-1" role="group" aria-label="Basic example">
        <button v-on:click="anterior" type="button" class="btn btn-primary" :disabled="inicio <= 0">
            Anterior {{ inicio }}
        </button>
        <button v-on:click="siguiente" type="button" class="btn btn-primary" :disabled="fin >= total">
            Siguiente {{ fin }}
        </button>
    </div>
</template>
<style></style>