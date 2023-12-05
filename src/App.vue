<template>
  <div class="container">
    <h1>APP</h1>
    <h2>Mis posts favs: {{ fav }}</h2>

    <PaginationPost @prevAction="prevAction" @nextAction="nextAction" :start="start" :end="end" :maxLength="maxLength" class="mb-2" />

    <BlogPost
      v-for="post in posts.slice(start, end)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @favHandler="changeFav"
      class="mb-2"
    />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import BlogPost from "./components/BlogPost.vue";
import PaginationPost from "./components/PaginationPost.vue";

const posts = ref([]);
const fav = ref("");

const postPerPage = 10;
const start = ref(0);
const end = ref(postPerPage);

const maxLength = computed(() => posts.value.length);

const changeFav = (title) => {
  fav.value = title;
};

const nextAction = () => {
  start.value = start.value + postPerPage;
  end.value = end.value + postPerPage;
};

const prevAction = () => {
  start.value = start.value - postPerPage;
  end.value = end.value - postPerPage;
};

fetch("https://jsonplaceholder.typicode.com/posts")
  .then((resp) => resp.json())
  .then((data) => (posts.value = data));
</script>
