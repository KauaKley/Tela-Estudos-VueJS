<script>
export default {
  props: {
    current: { type: Number, required: true },
    total: { type: Number, required: true }
  },
  emits: ['change-page']
};
</script>

<template>
  <nav class="actions" aria-label="Páginas dos produtos">
    <button type="button" :disabled="current <= 1" @click="$emit('change-page', current - 1)">Anterior</button>
    <button v-for="page in total" :key="page" type="button" :class="{ active: page === current }"
      :aria-current="page === current ? 'page' : 'false'" @click="$emit('change-page', page)">{{ page }}</button>
    <button type="button" :disabled="current >= total" @click="$emit('change-page', current + 1)">Próxima</button>
  </nav>
</template>
