<script setup>
  import { ref, computed, onMounted } from "vue";
  import blogPost from './components/blogPost.vue';
  import paginatePost from "./components/paginatePost.vue";
  import loadingSpinner from "./components/loadingSpinner.vue";

  const posts = ref([]);
  const myFavorite = ref("");
  const postxpage = 10;
  const inicio = ref(0);
  const fin = ref(postxpage);
  const loading = ref(false);

  onMounted(async () => {
    loading.value = true;
    try{
      const res = await fetch("https://jsonplaceholder.typicode.com/posts");
      posts.value = await res.json();
    }catch(error){
      console.log(error);
    }finally{
      setTimeout(() => (loading.value = false), 1500);
    }
  });

  const setFavorite = (dato)=>{
    myFavorite.value = dato;
  }

  const next = () => {
    inicio.value = inicio.value + postxpage;
    fin.value = fin.value + postxpage;
  }

  const prev = () => {
    inicio.value = inicio.value - postxpage;
    fin.value = fin.value - postxpage;
  }

  const maxLength = computed(() => posts.value.length);
</script>

<template>
  <loadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>{{ myFavorite || "Sin favorito" }}</h1>
    <paginatePost 
      @next="next"
      @prev="prev"
      :inicio="inicio"
      :fin="fin"
      :maxLength="maxLength"
      class="mb-2" />

    <blogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      class="mb-2"
      @setFavorite="setFavorite" />
  </div>
</template>