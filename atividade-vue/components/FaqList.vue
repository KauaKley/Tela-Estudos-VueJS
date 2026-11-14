<script>
export default {
  props: { items: { type: Array, required: true } },
  data() {
    return { aberto: -1 };
  },
  methods: {
    alternar(indice) {
      this.aberto = this.aberto === indice ? -1 : indice;
    }
  }
};
</script>

<template>
  <div v-for="(item, indice) in items" :key="item.title" class="faq-item">
    <button type="button" :aria-expanded="aberto === indice" @click="alternar(indice)">{{ item.title }}</button>
    <div class="fold" :class="{ open: aberto === indice }"><div><p>{{ item.body }}</p></div></div>
  </div>
</template>
