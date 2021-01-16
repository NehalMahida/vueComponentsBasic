<template>
  <div v-if="componentName === 'ProductDetails'">
    <h1 style="text-align: center;">Product Details</h1>
    <div class="productDetails">
      <div class="left">
        <div class="imgDiv">
          <img :src="product.imageSrc" alt="" />
        </div>
      </div>
      <div class="right">
        <p class="productName">{{ product.name }}</p>
        <p class="productDescription">{{ product.description }}</p>
        <p class="productPrice">RS. {{ product.price }}</p>

        <button type="button" class="btn btn-success" @click="goToEdit">
          Edit
        </button>
        <button type="button" class="btn btn-danger" @click="deleteProduct">
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    componentName: String, // this flag is used to keep track of active page on this website.
  },
  data: () => ({
    product: null,
  }),
  methods: {
    // click on a edit button.
    goToEdit() {
      // emit ProductEdit event so that on edit page it can listen and recieve the current product data.
      this.emitter.emit("productEdit", {
        product: this.product,
        componentName: "ProductEdit",
      });
      this.emitter.emit("backToHome", "ProductEdit");
    },
    // click on a delete button.
    deleteProduct() {
      if (confirm("Are you sure you want to delete this product?")) {
        this.emitter.emit("deleteProduct", this.product);
        this.emitter.emit("backToHome", "Products");
      }
    },
  },
  created() {
    // hooks to actively listen the event.
    this.emitter.on("productSelected", (product) => {
      this.product = product.product;
    });
  },
};
</script>

<style scoped>
.productDetails {
  display: flex;
  flex-direction: row;
  margin: 0 auto;
  width: 70%;
  box-shadow: 4px 4px 4px 0 rgba(0, 0, 0, 0.2);
  background-color: #fff;
  border-radius: 10px;
  padding-top: 5px;
}
.left {
  padding: 20px;
}
.imgDiv {
  width: 300px;
  height: 300px;
  margin-bottom: 10px;
}
.imgDiv img {
  max-width: 100%;
  max-height: 100%;
}
.right {
  padding: 20px;
}
/* img {
  max-width: 100%;
  max-height: 100%;
} */
.productName {
  font-size: 30px;
  font-weight: bold;
}
.productPrice {
  font-weight: bold;
}
.right button {
  margin-right: 10px;
}
</style>
