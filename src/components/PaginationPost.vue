<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button type="button" class="btn btn-outline-primary" @click="emit('prevAction')" :disabled="start === 0">Previous</button>
    <button type="button" class="btn btn-outline-primary" @click="emit('nextAction')" :disabled="end === maxLength">Next</button>
  </div>
</template>

<script setup>
defineProps({
  start: { type: Number, default: 0 },
  end: { type: Number },
  maxLength: { type: Number },
});

const emit = defineEmits(["prevAction", "nextAction"]);
</script>
