<template>
  <div>
    <p>Paginas{{ productsByPage }} {{ productsTotal }}</p>
  </div>
</template>

<script>
export default {
  name: "ProdutosPaginar",
  props: {
    productsByPage: {
      type: Number,
      default: 1,
    },
    productsTotal: {
      type: Number,
      default: 1,
    },
  },

  data() {
    return {};
  },

  methods: {},
};
</script>

<style></style>
