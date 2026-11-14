<script>
import dados from './dados.js';
import FaqList from './components/FaqList.vue';
import PageNav from './components/PageNav.vue';
import UploadProgress from './components/UploadProgress.vue';
import InfoTabs from './components/InfoTabs.vue';
import CategoryMenu from './components/CategoryMenu.vue';
import AppToast from './components/AppToast.vue';

const moeda = new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' });

export default {
  components: { FaqList, PageNav, UploadProgress, InfoTabs, CategoryMenu, AppToast },
  data() {
    return { dados, categoria: 'Todos', pagina: 1, progresso: 35 };
  },
  computed: {
    produtos() {
      return this.dados.products.filter(produto =>
        this.categoria === 'Todos' || produto.category === this.categoria
      );
    },
    total() {
      return Math.ceil(this.produtos.length / 2);
    },
    produtosDaPagina() {
      const inicio = (this.pagina - 1) * 2;
      return this.produtos.slice(inicio, inicio + 2);
    }
  },
  methods: {
    filtrar(categoria) {
      this.categoria = categoria;
      this.pagina = 1;
    },
    formatarPreco(valor) {
      return moeda.format(valor);
    }
  }
};
</script>

<template>
<main>
  <header><h1>Catálogo de estudo</h1><div>Vue.js</div></header>
  <div class="grid">
    <section>
      <h2>Perguntas frequentes</h2>
      <FaqList :items="dados.faq" />
    </section>
    <section>
      <h2>Produtos</h2>
      <ul><li v-for="produto in produtosDaPagina" :key="produto.name">{{ produto.name }} — {{ formatarPreco(produto.price) }}</li></ul>
      <PageNav :current="pagina" :total="total" @change-page="pagina = $event" />
    </section>
    <section>
      <h2>Progresso do envio</h2>
      <label for="envio">Simular andamento</label>
      <input id="envio" v-model.number="progresso" type="range" min="0" max="100">
      <UploadProgress :value="progresso" />
    </section>
    <section>
      <h2>Informações</h2>
      <InfoTabs :items="dados.tabs" />
    </section>
    <section>
      <h2>Categoria</h2>
      <CategoryMenu :options="dados.options" @select="filtrar" />
      <p>Filtro atual: {{ categoria }}</p>
    </section>
    <section>
      <h2>Notificação</h2>
      <AppToast />
    </section>
  </div>
</main>
</template>
