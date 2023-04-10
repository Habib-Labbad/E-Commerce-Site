<template>
  <div id="nav-bar">
    <router-link to="/products" id="products-link">
      <h1>FABULOUS FOOTWEAR</h1>
    </router-link>
    <router-link to="/cart" id="cart-link">
      <button>Shopping Cart</button>
    </router-link>
  </div>
</template>

<script>
export default {
  name: "NavBar",
};
</script>

<style scoped>
#nav-bar {
  border-bottom: 1px solid #ddd;
  height: 100px;
  width: 100%;
  display: flex;
}

#products-link {
  text-align: left;
  padding-left: 55px;
  color: black;
  font-size: 20px;
  text-decoration: none;
  width: 80%;
}

#cart-link {
  padding-top: 22px;
  padding-right: 20px;
  top: 16px;
  width: 20%;
}
</style>