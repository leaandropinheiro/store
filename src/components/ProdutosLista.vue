<template>
  <section class="produtos-container">
    <div v-if="products && products.length" class="produtos">
      <div class="produto" v-for="(product, index) in products" :key="index">
        <router-link to="/">
          <!-- <img
            v-if="product.fotos"
            src="product.fotos[0].src"
            alt="product.fotos[0].titulo"
          /> -->
          <h2 class="titulo">
            {{ product.name }}
          </h2>
          <p class="preco">
            {{ product.price }}
          </p>
          <p class="descricao">
            {{ product.description }}
          </p>
        </router-link>
      </div>
      <ProdutosPaginar
        :productsTotal="productsTotal"
        :productsByPage="productsByPage"
      />
    </div>
    <div v-else-if="products && products.length === 0" class="sem-resultados">
      <p>Busca sem resultados. Tente buscar outro termo.</p>
    </div>
  </section>
</template>

<script>
import { api } from "@/services.js";
import { serialize } from "@/helpers.js";
import ProdutosPaginar from "@/components/ProdutosPaginar.vue";

export default {
  name: "ProdutosLista",
  data() {
    return {
      products: null,
      productsByPage: this.productsTotal,
      productsTotal: 0,
    };
  },
  components: {
    ProdutosPaginar,
  },
  computed: {
    url() {
      const query = serialize(this.$route.query);
      return `/products?_limit=${this.productsByPage}${query}`;
    },
  },
  methods: {
    getProducts() {
      api.get(this.url).then((response) => {
        this.productsTotal = response.data.length;
        console.log("👉 response => ", response);
        this.products = response.data;
      });
    },
  },
  watch: {
    url() {
      this.getProducts();
    },
  },
  created() {
    this.getProducts();
  },
};
</script>

<style scoped>
.produtos-container {
  max-width: 1000px;
  margin: 0 auto;
}
.produtos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 30px;
  margin: 30px;
}

.produto {
  box-shadow: 0 4px 8px rgba(30, 60, 90, 0.1);
  padding: 10px;
  background: #fff;
  border-radius: 5px;
  transition: all 0.2s;
}
.produto:hover {
  box-shadow: 0 6px 12px rgba(30, 60, 90, 0.2);
  transform: scale(1.2);
  position: relative;
  z-index: 1;
}

.produto img {
  border-radius: 4px;
  margin-bottom: 10px;
}

.preco {
  font-weight: bold;
  color: #e80;
}

.sem-resultados {
  text-align: center;
}

@media screen and (max-width: 1336px) {
  .produtos {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media screen and (max-width: 768px) {
  .produtos {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 500px) {
  .produtos {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
