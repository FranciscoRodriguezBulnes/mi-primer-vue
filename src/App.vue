<script setup>
  import { ref, computed, onMounted } from 'vue';

  import ButtonCounter from './components/ButtonCounter.vue';
  import BlogPost from './components/BlogPost.vue';
  import PaginatePost from './components/PaginatePost.vue';
  import LoadingSpinner from './components/LoadingSpinner.vue';

  const posts = ref([]);
  const postXpage = 10;
  const inicio = ref(0);
  const fin = ref(postXpage);
  const loading = ref(true);

  const next = () => {
    inicio.value += postXpage;
    fin.value += postXpage;
  };
  const previous = () => {
    inicio.value -= postXpage;
    fin.value -= postXpage;
  };

  const postFavorito = ref('');

  const cambiarFavorito = (post) => {
    postFavorito.value = post;
  };

  // Utilizo esta alternativa si mecesito algo del DOM para har algo que dependa de algo del template pe getElementById

  // onMounted(async () => {
  //   try {
  //     const res = await fetch('https://jsonplaceholder.typicode.com/posts');
  //     posts.value = await res.json();
  //   } catch (error) {
  //     console.log(error);
  //   } finally {
  //     setTimeout(() => {
  //       loading.value = false;
  //     }, 2000);
  //   }
  // });

  // fetch('https://jsonplaceholder.typicode.com/posts')
  //   .then((res) => res.json())
  //   .then((data) => {
  //     posts.value = data;
  //   })
  //   .catch((e)=> console.log(e))
  //   .finally(() => {
  //     setTimeout(()=>{
  //       loading.value = false

  //     },2000 )
  //   })

  //la mejor alternativa

  const fetchData = async () => {
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/posts');
      posts.value = await res.json();
    } catch (error) {
      console.log(error);
    } finally {
      setTimeout(() => {
        loading.value = false;
      }, 2000);
    }
  };

  fetchData()

  const maxLengtC = computed(() => posts.value.length);
</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>APP Vue</h1>
    <!-- <ButtonCounter />
    <button-counter /> -->
    <h2>Mis Posts Favoritos: {{ postFavorito }}</h2>

    <!-- <button @click="next">Next Provisional</button> -->
    <!-- <button @click="previous">Previous Provisional</button> -->

    <PaginatePost
      @next="next"
      @previous="previous"
      :inicio="inicio"
      :fin="fin"
      :maxLength="posts.length"
      class="mb-2"
    />

    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title"
      :body="post.body"
      :id="post.id"
      :colorText="post.colorText"
      @cambiarFavoritoNombre="cambiarFavorito"
      class="mb-2"
    >
    </BlogPost>
  </div>
</template>

<style></style>
