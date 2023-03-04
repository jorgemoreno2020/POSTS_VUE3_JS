<script setup>

defineProps(['inicio','final','Postlen'])
const emit= defineEmits(['previous','next'])

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
    <button @click="$emit('previous')" type="button" 
    :disabled="inicio<=0" class="btn btn-primary" >Previous {{ inicio }}</button>
    <button @click="$emit('next')" type="button" :disabled="final>=Postlen" class="btn btn-primary">Next {{ final }}</button>
</div>
</template>