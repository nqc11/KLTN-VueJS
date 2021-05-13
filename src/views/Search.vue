<template>
  <NavBar />

  <div class="pt-5 pb-5">
    <h4 class="title text-uppercase">Tìm Kiếm</h4>
    <div class="container">
      <div class="row">
        <div v-if="!products.length" class="col">
          <Loading />
        </div>
        <div v-for="product in products" :key="product.id" class="col-3">
          <ItemProduct v-bind:product="product"></ItemProduct>
        </div>
      </div>
    </div>
  </div>
  <Footer />
</template>

<script>
// import axios from "axios";
import NavBar from "../components/commons/NavBar";
import Footer from "../components/commons/Footer";
import ItemProduct from "../components/ItemProduct";
import Loading from "../components/commons/Loading";
import { productService } from "../services/index";

export default {
  name: "ListProduct",
  components: {
    ItemProduct,
	Loading,
	NavBar,
	Footer
  },
  data() {
    return {
      products: [],
    };
  },
  methods() {},
  created() {
    productService
      .search(this.$route.query.keyword)
      .then((result) => {
        this.products = result.data.data;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  mounted() {},
};
</script>

<style scoped>
.title {
  margin-bottom: 20px;
  letter-spacing: 2px;
  color: #0e3a3b;
  font-weight: 700;
}
</style>
