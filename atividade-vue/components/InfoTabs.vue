<script>
export default {
  props: { items: { type: Array, required: true } },
  data() {
    return { ativa: 0 };
  }
};
</script>

<template>
  <div class="actions">
    <button v-for="(item, indice) in items" :key="item.title" type="button"
      :class="{ active: ativa === indice }" :aria-pressed="ativa === indice"
      @click="ativa = indice">{{ item.title }}</button>
  </div>
  <p>{{ items[ativa].body }}</p>
</template>
