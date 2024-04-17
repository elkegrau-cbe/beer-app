<template>
  <div id="app">
    <header>
      <h1>Bierparadies</h1>
      <img
        src="@/assets/bierkrug.png"
        alt="Bierkrug"
        height="150px"
        width="150px"
      />
    </header>
    <SortOptions @sort="handleSort" />
    <ProductList :sortedProducts="sortedProducts" />
    <footer>
      <p>&copy; 2024 Bier App</p>
    </footer>
  </div>
</template>

<script>
//import SortOptions from "@/components/SortOptions.vue";//
import ProductList from "@/components/ProductList.vue";

export default {
  name: "App",
  components: {
    //SortOptions,//
    ProductList,
  },
  data() {
    return {
      sortedProducts: [],
    };
  },
  methods: {
    handleSort(option) {
      // Implement sorting logic here
      console.log("Sort option selected:", option);
    },
  },
};
</script>

<style>
body {
  background-color: antiquewhite;
}
#app {
  font-family: Arial, sans-serif;
  margin: 0 auto;
  padding: 20px;
  max-width: 800px;
  text-align: center;
}
header {
  text-align: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  margin-bottom: 30px;
}
footer {
  text-align: center;
  margin-top: 40px;
  font-size: small;
}
</style>
