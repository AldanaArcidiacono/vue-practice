<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ id }} - {{ title }}</h5>
      <p>{{ body }}</p>
      <button @click="$emit('favHandler', title)" class="btn btn-outline-primary">FAV</button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: "No desc",
  },
});

const emit = defineEmits(["favHandler"]);
</script>
