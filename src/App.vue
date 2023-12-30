<template>
  <AddProduct @add:product="addProduct" />
  <ProductList
    @update:product="updateProduct"
    @delete:product="deleteProduct"
    :products="products"
  />
</template>

<script>
import AddProduct from "./components/AddProduct.vue";
import ProductList from "./components/ProductList.vue";

export default {
  name: "App",
  components: {
    ProductList,
    AddProduct,
  },
  data() {
    return {
      products: [],
      visibile : false
    };
  },
  mounted() {
    this.getProducts();
  },
  methods: {
    async getProducts() {

      const result = await fetch("http://localhost:3000/products", {
        method: "GET",

      });
      const data = await result.json();
      this.products = data;
    },

    async deleteProduct(product) {

      await fetch("http://localhost:3000/products/" + product.id, {
        method: "DELETE",
      });

      this.products = this.products.filter((b) => b.id !== product.id);

    },

    async updateProduct(product) {

      const result = await fetch("http://localhost:3000/products/" + product.id, {
        method: "PUT",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });

      const updatedProduct = await result.json()

      this.products = this.products.map((product) => product.id === updatedProduct.id ? updatedProduct : product)

    },  

    async addProduct(product) {

      const result = await fetch("http://localhost:3000/products", {
        method: "POST",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });

      const newProduct = await result.json();
      this.products = [...this.products, newProduct];

      window.location.reload();
    }
    
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
