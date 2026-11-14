<script>
export default {
  data() {
    return { mensagem: '', timer: null };
  },
  beforeUnmount() {
    this.fechar();
  },
  methods: {
    mostrar() {
      this.fechar();
      this.mensagem = 'Preferências salvas na simulação.';
      this.timer = setTimeout(this.fechar, 3500);
    },
    fechar() {
      clearTimeout(this.timer);
      this.mensagem = '';
    }
  }
};
</script>

<template>
  <button type="button" @click="mostrar">Simular salvamento</button>
  <div v-if="mensagem" class="toast">
    <span role="status">{{ mensagem }}</span>
    <button type="button" @click="fechar">Fechar</button>
  </div>
</template>
