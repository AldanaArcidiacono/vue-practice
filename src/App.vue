<template>
  <LoadingSpinner v-if="loading" />

  <div class="container" v-else>
    <h1>Harry Potter WIKI</h1>
    <h2>My favorite Wizard: {{ fav }}</h2>

    <PaginationPost @prevAction="prevAction" @nextAction="nextAction" :start="start" :end="end" :maxLength="maxLength" class="mb-2" />

    <WizardPost
      v-if="wizardingWorld"
      v-for="wizard of wizardingWorld.personajes.slice(start, end)"
      :wizard="wizard"
      @favHandler="changeFav"
      class="mb-2"
    />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import WizardPost from "./components/WizardPosts.vue";
import PaginationPost from "./components/PaginationPost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const fav = ref("");
const loading = ref(true);
const wizardingWorld = ref([]);

const postPerPage = 5;
const start = ref(0);
const end = ref(postPerPage);

const maxLength = computed(() => wizardingWorld.value.personajes.length);

const changeFav = (nickName) => {
  fav.value = nickName;
};

const nextAction = () => {
  start.value = start.value + postPerPage;
  end.value = end.value + postPerPage;
};

const prevAction = () => {
  start.value = start.value - postPerPage;
  end.value = end.value - postPerPage;
};

const fetchData = () => {
  fetch("https://harry-potter-api.onrender.com/db")
    .then((resp) => resp.json())
    .then((data) => (wizardingWorld.value = data))
    .finally(() => (loading.value = false));
};

onMounted(async () => {
  fetchData();
});
</script>
