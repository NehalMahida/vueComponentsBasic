<template>
  <li>
    <div class="left">
      <div class="imgDiv">
        <img :src="product.imageSrc" alt="" @click="productSelected" />
      </div>
    </div>
    <div class="right">
      <p class="productName">{{ product.name }}</p>
      <p class="productDescription">{{ product.description }}</p>
      <p class="productPrice">RS. {{ product.price }}</p>
      <button type="button" class="btn btn-primary" @click="productSelected">
        Show
      </button>
      <button type="button" class="btn btn-success" @click="productEdit">
        Edit
      </button>
      <button type="button" class="btn btn-danger" @click="productDelete">
        Delete
      </button>
    </div>
  </li>
</template>

<script>
export default {
  props: ["product"],
  methods: {
    // when product selected from list, pass the current product data to productDetails page.
    productSelected() {
      this.emitter.emit("productSelected", {
        product: this.product,
        componentName: "ProductDetails",
      });
    },
    // when click on edit button.
    productEdit() {
      this.emitter.emit("productEdit", {
        product: this.product,
        componentName: "ProductEdit",
      });
    },
    // when click on delete button.
    productDelete() {
      if (confirm("Are you sure you want to delete this product?")) {
        this.emitter.emit("deleteProduct", this.product);
        this.emitter.emit("backToHome", "Products");
      }
    },
  },
};
</script>

<style scoped>
.left {
  padding: 10px;
}
.imgDiv {
  width: 200px;
  height: 200px;
}
.imgDiv img {
  max-width: 100%;
  max-height: 100%;
}
li {
  margin: 10px auto;
  width: 50%;
  display: flex;
  flex-direction: row;
  box-shadow: 4px 4px 4px 0 rgba(0, 0, 0, 0.2);
  background-color: #fff;
  border-radius: 10px;
  padding-top: 5px;
}
button {
  margin: 10px 5px 10px 0;
}
.productName {
  font-weight: bold;
  font-size: 20px;
}

.productPrice {
  margin-top: 5px;
  margin-bottom: 10px;
  font-weight: bold;
}
</style>
