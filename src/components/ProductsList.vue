<template>
  <ul v-if="componentName === 'Products'">
    <my-product
      v-for="product in products"
      :key="product.id"
      :product="product"
    >
    </my-product>
  </ul>
</template>

<script>
import Product from "./Product";

export default {
  props: {
    componentName: String,
  },
  data: () => ({
    products: {
      0: {
        id: 0,
        name: "Computer",
        description:
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
        price: 12000,
        imageSrc: require("../assets/computer.jpg"),
      },
      1: {
        id: 1,
        name: "Laptop",
        description:
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
        price: 20000,
        imageSrc: require("../assets/laptop.jpg"),
      },
      2: {
        id: 2,
        name: "Keyboard",
        description:
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
        price: 1200,
        imageSrc: require("../assets/keyboard.jpg"),
      },
      3: {
        id: 3,
        name: "CPU",
        description:
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
        price: 8000,
        imageSrc: require("../assets/cpu.jpg"),
      },
      4: {
        id: 4,
        name: "Mouse",
        description:
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
        price: 120,
        imageSrc: require("../assets/mouse.jpg"),
      },
    },
  }),
  components: {
    "my-product": Product,
  },
  created() {
    // when delete event occues. delete data from here.
    this.emitter.on("deleteProduct", (product) => {
      delete this.products[product.id];
    });

    // update products data.
    this.emitter.on("updateProduct", (product) => {
      console.log("Update product", product);
      this.products[product.id] = product;
    });
  },
};
</script>

<style scoped>
ul {
  padding-bottom: 50px;
}
</style>
