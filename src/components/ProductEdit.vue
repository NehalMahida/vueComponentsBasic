<template>
  <div v-if="componentName === 'ProductEdit'">
    <h1 style="text-align: center;">Edit Product</h1>
    <div class="productEdit">
      <div class="left">
        <div class="imgDiv">
          <img :src="copyProduct.imageSrc" alt="" />
        </div>
        <input
          type="file"
          id="inputFile"
          @change="uploadImg"
          accept=".png,.jpg,.jpeg"
          hidden
        />
        <label for="inputFile" class="btn btn-dark">Upload</label>
      </div>
      <div class="right">
        <form action="" @submit="updateProduct">
          <div class="inputField">
            <label for="productName">Product Name</label> <br />
            <input type="text" id="productName" v-model="copyProduct.name" />
          </div>
          <div class="inputField">
            <label for="productDescription">Product Description</label> <br />
            <textarea
              name="productDescription"
              id="productDescription"
              cols="50"
              rows="5"
              v-model="copyProduct.description"
            ></textarea>
          </div>
          <div class="inputField">
            <label for="productPrice">Product Price (In Rupees)</label> <br />
            <input
              type="number"
              id="productPrice"
              v-model="copyProduct.price"
              min="0"
            />
          </div>
          <input type="submit" class="btn btn-success" value="Save" />
          <button type="button" class="btn btn-danger" @click="cancelUpdate">
            Cancel
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    componentName: String,
  },
  data: () => ({
    product: null,
    copyProduct: new Map(), // copy product is used when user choose to cancel product update. so we can put it back to original data.
  }),
  methods: {
    // click on update button.
    updateProduct(e) {
      alert("Product Details Updated Successfully");
      this.product = this.copyProduct;
      this.emitter.emit("updateProduct", this.product);
      this.emitter.emit("backToHome", "Products");
      e.preventDefault();
    },
    // click on cancel update.
    cancelUpdate() {
      alert("Update Cancel!!");
      this.emitter.emit("backToHome", "Products");
    },
    // when click on upload button.
    uploadImg(e) {
      // logic to render image in img tag.
      const file = e.target.files[0];
      const reader = new FileReader();
      reader.onload = (event) => {
        this.copyProduct.imageSrc = event.target.result;
      };
      reader.readAsDataURL(file);
    },
  },
  created() {
    this.emitter.on("productEdit", (product) => {
      this.product = product.product;
      // this because if I directly assign the value to copyProduct it will use SwallowCopy so the cancel update login will no work
      // by doing this you can do DeepCopy where both are habing diffrent memory addresses.
      this.copyProduct = JSON.parse(JSON.stringify(this.product));
    });
  },
};
</script>

<style scoped>
.productEdit {
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
  text-align: center;
  display: flex;
  flex-direction: column;
  padding: 20px;
}
.right {
  padding: 20px;
}
.inputField {
  margin-bottom: 10px;
}
.inputField label {
  font-weight: bold;
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
.productName {
  font-size: 30px;
  font-weight: bold;
}
.productPrice {
  font-weight: bold;
}
.left button {
  margin: 20px 0;
}
.right button {
  margin-top: 25px;
  margin-right: 10px;
}
input[type="submit"] {
  margin-top: 25px;
  margin-right: 10px;
}
</style>
