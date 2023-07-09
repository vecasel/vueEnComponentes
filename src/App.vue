<script setup>

  import {ref, onMounted, computed} from 'vue';
  
  import BlogPost from './components/BlogPost.vue';
  import PaginatePost from './components/PaginatePost.vue';
  import LoadingSpinner from './components/LoadingSpinner.vue';

  
  const posts = ref([]);
  let postsLenght = 0;

  onMounted(async() =>{
    try{
      const res = await fetch('https://jsonplaceholder.typicode.com/posts');
      posts.value = await res.json();
      postsLenght = posts.value.length; 
    }
    catch(error){
      console.log(error)
    }
    finally{
      setTimeout(() => {
        loading.value = false;
      }, 2000);
    }
  });


  /*fetch('https://jsonplaceholder.typicode.com/posts')
    .then(res => res.json())
    .then(data => {
      posts.value = data
      postsLenght = Object.keys(data).length;
    })
    .catch(e => console.log(e))
    .finally(() => loading.value = false);*/

  const loading = ref(true);
  const favorito = ref("");
  const postXPagina = 10;
  const inicio = ref(0);
  const fin = ref(postXPagina);


  const next = () => {
    inicio.value += postXPagina;
    fin.value += postXPagina;
  }

  const prev = () => {
    inicio.value += -postXPagina;
    fin.value += -postXPagina;
  }

  const cambiarFavorito = (title) => favorito.value = title;



</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mis Post Favoritos: {{ favorito }} {{ postsLenght }}</h2>

    <PaginatePost 
      class="mb-2"
      @next="next"
      @prev="prev"
      :inicio="inicio"
      :fin="fin"
      :postsLenght="postsLenght"
    >
    </PaginatePost>

    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @cambiarFavoritoPrueba="cambiarFavorito"
      class="mb-2"
    >  
    </BlogPost>
  </div>
  
</template>