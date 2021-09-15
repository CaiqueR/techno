<template>
  <section class="produtos">
    <div v-for="produto in produtos" :key="produto.id" class="produto">
      <img :src="produto.img" :alt="produto.nome" class="produto_img" />

      <div class="produto_info">
        <span class="produto_preco">{{ produto.preco }}</span>
        <h2 class="produto_titulo">{{ produto.nome }}</h2>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Main",
  data() {
    return {
      produtos: [],
    };
  },
  methods: {
    async fetchProdutos() {
      const response = await fetch("./api/produtos.json");
      const produtos = await response.json();
      this.produtos = produtos;
    },
  },
  created() {
    this.fetchProdutos();
  },
};
</script>

<style scoped>
.produtos {
  max-width: 900px;
  margin: 100px auto 0 auto;
}

.produto {
  display: flex;
  align-items: center;
  margin-bottom: 40px;
  background: #fff;
  box-shadow: 0 0 2rem rgba(0, 0, 0, 0.1);
}

.produto_img {
  max-width: 300px;
  margin-right: 40px;
}

.produto_titulo {
  font-size: 3rem;
  line-height: 1;
}

.produto_preco {
  color: rgba(0, 0, 0, 0.5);
}
</style>
