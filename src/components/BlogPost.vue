<script setup>
// defineProps(['title', 'body', 'id', 'textColor']);

defineProps({
    title: String,
    id: {
        type: Number,
        default: 0
    },
    body: {
        type: String,
        default: 'Sin descripcion'
    },
    textColor: String
});

// const myEmit = defineEmits(['miPostFavorito']);
const myEmit = defineEmits({
    miPostFavorito(title){
        console.log(title);
        return true;
    }
});





</script>

<template>
    <div class="card">
        <div class="card-body">
            <h6 class="card-subtitle mb-2 text-muted">
                # {{ id }}
            </h6>
            <h5 class="card-title">
                {{ title }}
            </h5>
            <p> {{ body }} </p>            
            <button v-on:click="myEmit('miPostFavorito', title)" type="button" class="btn btn-primary btn-sm"> Favorito </button>
        </div>
    </div>
</template>

<style></style>