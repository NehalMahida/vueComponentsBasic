<template>
  <div>
    <Header :componentName="componentName"></Header>
    <Products :componentName="componentName"></Products>
    <ProductDetails :componentName="componentName"></ProductDetails>
    <ProductEdit :componentName="componentName"></ProductEdit>
    <Footer></Footer>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import Header from "./components/Header";
import Products from "./components/ProductsList";
import ProductDetails from "./components/ProductDetails";
import ProductEdit from "./components/ProductEdit";
import Footer from "./components/Footer";

export default {
  name: "App",
  data: () => ({
    componentName: "Products",
  }),
  components: {
    Header,
    Products,
    ProductDetails,
    ProductEdit,
    Footer,
  },
  created() {
    // the below event listeners are used to check active pages.
    this.emitter.on("productSelected", (product) => {
      this.componentName = product.componentName;
    });
    this.emitter.on("productEdit", (product) => {
      this.componentName = product.componentName;
    });
    this.emitter.on("backToHome", (componentName) => {
      this.componentName = componentName;
    });
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  background-color: #eee;
}
</style>
