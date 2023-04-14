<script setup>
import { ref } from 'vue'

const contador = ref(0);

const incrementarContador = (estado) => estado ? contador.value++ : contador.value--;

</script>
<template>
    <div class="btn-group">
        <button v-on:click="incrementarContador(true)" class="btn btn-primary"> + </button>
        <p class="form-control mb-0">{{ contador }}</p>
        <button v-on:click="incrementarContador(false)" class="btn btn-primary"> - </button>
    </div>
</template>
<style></style>
