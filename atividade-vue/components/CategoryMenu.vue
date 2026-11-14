<script>
export default {
  props: { options: { type: Array, required: true } },
  emits: ['select'],
  data() {
    return { aberto: false };
  },
  mounted() {
    document.addEventListener('click', this.fecharFora);
  },
  beforeUnmount() {
    document.removeEventListener('click', this.fecharFora);
  },
  methods: {
    fecharFora(evento) {
      if (!this.$el.contains(evento.target)) this.aberto = false;
    },
    selecionar(opcao) {
      this.aberto = false;
      this.$emit('select', opcao);
    }
  }
};
</script>

<template>
  <div class="dropdown">
    <button type="button" :aria-expanded="aberto" @click="aberto = !aberto">Escolher categoria</button>
    <div v-if="aberto" class="options">
      <button v-for="opcao in options" :key="opcao" type="button" @click="selecionar(opcao)">{{ opcao }}</button>
    </div>
  </div>
</template>
