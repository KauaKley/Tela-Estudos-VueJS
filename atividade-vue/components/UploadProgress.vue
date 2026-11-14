<script>
export default {
  props: { value: { type: Number, required: true } }
};
</script>

<template>
  <progress max="100" :value="value" aria-label="Progresso do envio"></progress>
  <span>{{ value }}%</span>
</template>
