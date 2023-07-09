<script setup>
    //defineProps(['title', 'id', 'body'])
    defineProps({
        title: String,
        id: Number,
        body:{
            typeof: String,
            default: 'Sin Descripción'
        }
    })

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{id}} - {{title}}</h5>
            <p>{{body}}</p>
            <button 
                class="btn btn-outline-primary"
                @click="$emit('cambiarFavoritoPrueba', title)"
            >
                Favorito
            </button>
        </div>
    </div>
</template>