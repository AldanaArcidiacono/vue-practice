<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ wizard.id }} - {{ wizard.personaje }}</h5>

      <img :src="wizard.imagen" :alt="wizard.personaje" />

      <p v-if="wizard.estudianteDeHowarts">Howarts hose: {{ wizard.casaDeHogwarts }}</p>

      <p>Actor: {{ wizard.interpretado_por }}</p>

      <button @click="$emit('favHandler', wizard.apodo)" class="btn btn-outline-primary">FAV</button>
    </div>
  </div>
</template>

<script setup>
defineProps(["wizard"]);
const emit = defineEmits(["favHandler"]);
</script>
