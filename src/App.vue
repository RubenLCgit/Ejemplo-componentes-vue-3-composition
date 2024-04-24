<script setup>
  import { ref, computed, onMounted } from 'vue';

  import BlogPost from './components/BlogPost.vue';
  import PaginatePost from './components/PaginatePost.vue';
  import LoadingSpinner from './components/LoadingSpinner.vue';


  const posts = ref([]);
  const favorito = ref('');

  const cambiarFavorito = (title) => { 
    favorito.value = title;
  };

  const postXPage = 5;
  const initPost = ref(0);
  const endPost = ref(postXPage);
  const statePrevius = computed (() => initPost.value === 0);
  const stateNext = computed (() => endPost.value >= posts.value.length);

  const nextPost = () => {
    if (endPost.value < posts.value.length) {
      initPost.value += postXPage;
      endPost.value += postXPage;
    }
  };

  const previusPost = () => {
    if (initPost.value > 0) {
      initPost.value -= postXPage;
      endPost.value -= postXPage;
    }
  };

const loading = ref(false);

const fetchData = async () => {
  loading.value = true;
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    const data = await response.json();
    posts.value = data;
  } catch (error) {
    console.error('Error:', error);
  } finally {
    loading.value = false;
  }
};

onMounted(() => {
  fetchData();
});

</script>

<template>

  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mis Post Favoritos: {{ favorito }}</h2>

    <PaginatePost 
      class="mb-2"
      :statePrevius="statePrevius"
      :stateNext="stateNext"
      @nextPost="nextPost"
      @previusPost="previusPost"
    ></PaginatePost>

    <BlogPost
      v-for="item in posts.slice(initPost, endPost)"
      :key="item.id" 
      :title= "item.title" 
      :id="item.id" 
      :body="item.body" 
      :colorText="item.colorText"
      @cambiarNombreFavorito="cambiarFavorito"
    ></BlogPost>
  </div>

</template>

<style scoped>

</style>
