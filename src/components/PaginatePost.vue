<script setup>
    defineProps(['inicio', 'fin', 'postsLenght']);
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-secondary" @click="$emit('prev')" :disabled="inicio <= 0">Previous {{ inicio }}</button>
        <button type="button" class="btn btn-secondary" @click="$emit('next')" :disabled="fin >= postsLenght">Next {{ fin }}</button>
    </div>
</template>