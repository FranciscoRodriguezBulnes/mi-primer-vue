<script setup>
  import { ref } from 'vue';

  import ButtonCounter from './components/ButtonCounter.vue';
  import BlogPost from './components/BlogPost.vue';

  const posts = ref([
    { title: 'Post 1', id: 1, body: 'descripción 1', colorText: 'primary' },
    { title: 'Post 2', id: 2, body: 'descripción 2', colorText: 'secondary' },
    { title: 'Post 3', id: 3, body: 'descripción 3', colorText: 'success' },
  ]);

  const postFavorito = ref('');

  const cambiarFavorito = (post) => {
    postFavorito.value = post;
  };
</script>

<template>
  <div class="container">
    <h1>APP Vue</h1>
    <!-- <ButtonCounter />
    <button-counter /> -->
    <h2>Mis Posts Favoritos: {{ postFavorito }}</h2>

    <BlogPost
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      :body="post.body"
      :id="post.id"
      :colorText="post.colorText"
      @cambiarFavoritoNombre="cambiarFavorito"
    >
    </BlogPost>
  </div>
</template>

<style></style>
