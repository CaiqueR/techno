<template>
  <div>
    <section class="modal" v-if="produto.nome">
      <div class="modal_container">
        <div class="modal_img">
          <img :src="produto.img" :alt="produto.nome" />
        </div>
        <div class="modal_dados">
          <span class="modal_preco">{{ produto.preco }}</span>
          <h2 class="modal_titulo">{{ produto.nome }}</h2>
          <p>{{ produto.descricao }}</p>
          <button class="modal_btn">Adicionar Item</button>
        </div>
        <div class="avaliacoes">
          <h2 class="avaliacoes_subtitulo">Avaliações</h2>
          <ul>
            <li
              v-for="avaliacao in produto.reviews"
              :key="avaliacao.id"
              class="avaliacao"
            >
              <p class="avaliacao_descricacao">{{ avaliacao.descricao }}</p>
              <p class="avaliacao_usuario">
                {{ avaliacao.nome }} | {{ avaliacao.estrelas }}
              </p>
            </li>
          </ul>
        </div>
      </div>
    </section>

    <section class="produtos">
      <div
        v-for="produto in produtos"
        @click="fetchProduto(produto.id)"
        :key="produto.id"
        class="produto"
      >
        <img :src="produto.img" :alt="produto.nome" class="produto_img" />

        <div class="produto_info">
          <span class="produto_preco">{{ produto.preco | numeroPreco }}</span>
          <h2 class="produto_titulo">{{ produto.nome }}</h2>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "Main",
  data() {
    return {
      produtos: [],
      produto: { reviews: [] },
    };
  },
  filters: {
    numeroPreco(value) {
      return value.toLocaleString("pt-BR", {
        style: "currency",
        currency: "BRL",
      });
    },
  },
  methods: {
    async fetchProdutos() {
      const response = await fetch("./api/produtos.json");
      const produtos = await response.json();
      this.produtos = produtos;
    },
    async fetchProduto(id) {
      const response = await fetch(`./api/produtos/${id}/dados.json`);
      const produto = await response.json();
      this.produto = produto;
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
  cursor: pointer;
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

.modal::before {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
}

.modal {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  top: 0;
  left: 0;
  width: 100%;
  padding: 80px;
}

.modal_container {
  display: grid;
  align-items: end;
  grid-gap: 50px;
  padding: 0 50px 50px 0;
  position: relative;
  z-index: 1;
  background: linear-gradient(to right, transparent 250px, white 250px);
}

.modal_img {
  margin-top: 50px;
  box-shadow: 0px 3px 4px rgba(0, 0, 0, 0.1);
}

.modal_img img {
  max-width: 300px;
  display: block;
  grid-column: 1;
}

.modal_dados {
  grid-column: 2;
  max-width: 600px;
}

.modal_titulo {
  font-size: 3rem;
}

.modal_btn {
  margin-top: 80px;
  background: #000;
  cursor: pointer;
  color: #fff;
  border: none;
  font-size: 1rem;
  padding: 10px 25px;
  font-family: "Noto Serif";
}

.modal_btn:active {
  background: #808080;
}

.avaliacoes {
  grid-column: 2;
}

.avaliacao {
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  padding-bottom: 20px;
}

.avaliacao_descricacao {
  color: rgba(0, 0, 0, 0.7);
  margin: 20px 0 5px 0;
}

.avaliacoes_subtitulo {
  font-size: 1.75rem;
}

.avaliacao_usuario {
  font-weight: bold;
}
</style>
