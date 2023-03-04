<script setup>
import { ref, computed, onMounted } from "vue";

import BlogPost from "./components/BlogPost.vue";
import PagePost from "./components/PagePost.vue";
import PageLoading from "./components/PageLoading.vue";
const color = "color:blue";

/* fetch("https://jsonplaceholder.typicode.com/posts")  es la alternativa recomendada 
  .then(res=>res.json())
  .then(data=>posts.value=data)
  .finally(()=> loading.value=false) */
/*   .finally( ()=>{  Este setTimeout nos sirve para visualizar el sppiner
    setTimeout(()=>{
      loading.value=false
    },2000)
  }
    ) */

const posts = ref([]);
const postLen = computed(() => posts.value.length);
const pageFinal = 5; /* numero de post que tendra el articulo */
const inicio = ref(0);
const final = ref(pageFinal);
const loading = ref(true);

const miFavorito = ref("");
const fijarFavorito = (title) => (miFavorito.value = title);

const next = () => {
  inicio.value = inicio.value + pageFinal;
  final.value = final.value + pageFinal;
};

const previous = () => {
  inicio.value = inicio.value - pageFinal;
  final.value = final.value - pageFinal;
};

/* onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false;
  }
})

 */

/* la alternativa mas valida despues del fetch es el uso de un metodo */

const fetchData= async () =>{
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false;
  }
}

fetchData()


</script>

<template>
  <PageLoading v-if="loading"></PageLoading>

  <div class="container" v-else>
    <h1 :style="color">The best post {{ postLen }}</h1>
    <br />
    <PagePost
      @next="next"
      @previous="previous"
      :Postlen="postLen"
      :inicio="inicio"
      :final="final"
      class="mb-2"
    >
    </PagePost>
    <h2>Postales Favoritas: {{ miFavorito || "Sin favorito" }}</h2>
    <BlogPost
      v-for="post in posts.slice(inicio, final)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      :colorText="post.colorText"
      @fijarFavorito="fijarFavorito"
      class="mb-2"
    ></BlogPost>
  </div>
</template>
