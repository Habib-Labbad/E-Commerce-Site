<template>
  <div id="page-wrap" v-if="product">
    <div id="img-wrap">
      <img :src="product.imageUrl" alt="" />
    </div>
    <div id="product-details">
      <h1>{{ product.name }}</h1>
      <h3 id="price">${{ product.price }}</h3>
      <p>Average rating:{{ product.averageRating }}</p>
      <button
        v-if="!itemIsInCart && !showSuccesMessage"
        v-on:click="addToCart"
        id="add-to-cart"
      >
        Add to Cart
      </button>
      <button
        v-if="!itemIsInCart && showSuccesMessage"
        class="green-button"
        id="add-to-cart"
      >
        Successfully added button to cart!
      </button>
      <button v-if="itemIsInCart" class="grey-button" id="add-to-cart">
        Item is already in cart!
      </button>
      <h4>Description</h4>
      <p>{{ product.description }}</p>
    </div>
  </div>
  <NotFoundPage v-else />
</template>

<script>
import axios from "axios";
import NotFoundPage from "./NotFoundPage.vue";
export default {
  name: "ProductDetailPage",
  components: { NotFoundPage },
  data() {
    return {
      product: {},
      cartItems: [],
      showSuccesMessage: false,
    };
  },
  computed: {
    itemIsInCart() {
      return this.cartItems.some((item) => item.id === this.product.id);
    },
  },

  methods: {
    async addToCart() {
      await axios.post("/api/users/12345/cart", {
        productId: this.$route.params.id,
      });
      this.showSuccesMessage = true;
      setTimeout(() => {
        this.$router.push("products");
      }, 1500);
    },
  },
  async created() {
    const { data: product } = await axios.get(
      `/api/products/${this.$route.params.id}`
    );
    this.product = product;
    const { data: cartItems } = await axios.get("/api/users/12345/cart");
    this.cartItems = cartItems;
  },
};
</script>

<style scoped>
#page-wrap {
  margin-top: 16px;
  padding: 16px;
  max-width: 600px;
}

#img-wrap {
  text-align: center;
}

img {
  width: 400px;
}

#product-details {
  padding: 16px;
  position: relative;
}

#add-to-cart {
  width: 100%;
}

#price {
  position: absolute;
  top: 24px;
  right: 16px;
}

.green-button {
  background-color: green;
}

.grey-button {
  background-color: #888;
}
</style>