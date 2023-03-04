<script setup>
import {ref} from 'vue'
/* defineProps(['title','id','body','colorText']) */
defineProps({
    title:String,
    id:Number,
    body:{
        type:String,
        default:"With out description"
    },
    colorText:String
   /*  elegirFavorito:Function */
})

const emit= defineEmits(['fijarFavorito'])

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`"> {{ id }} - {{ title}} </h5>
            <p> {{ body }} </p>
            <button @click="$emit('fijarFavorito',title)" 
            class="btn btn-outline-primary">favorito</button>
        </div>
    </div>
</template>