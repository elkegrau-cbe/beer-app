<template>
  <div class="product-list">
    <div class="filters">
      <label for="sort-select">Sortiere nach Brauerei, Sorte oder Preis:</label>
      <select
        id="sort-select"
        v-model="selectedSortOption"
        @change="sortProducts"
      >
        <option value="name">Brauerei</option>
        <option value="category">Sorte</option>
        <option value="price">Preis</option>
      </select>
      <br />
      <br />
      <label for="category-select"
        >Du magst heute lieber ein Helles statt Pils? Dann kannst du hier
        filtern:</label
      >
      <select
        id="category-select"
        v-model="selectedCategory"
        @change="filterProducts"
      >
        <option value="">Alle</option>
        <option
          v-for="category in uniqueCategories"
          :key="category"
          :value="category"
        >
          {{ category }}
        </option>
      </select>
    </div>
    <div class="product-items">
      <div
        v-for="product in filteredProducts"
        :key="product.id"
        class="product-item"
      >
        <p>
          {{ product.name }} - {{ product.category }} - € {{ product.price }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      selectedSortOption: "name",
      selectedCategory: "", // Updated selectedCategory
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    fetchProducts() {
      fetch("/products.json")
        .then((response) => {
          if (!response.ok) {
            throw new Error("Network response was not ok");
          }
          return response.json();
        })
        .then((data) => {
          this.products = data;
        })
        .catch((error) => {
          console.error("Error fetching products:", error);
        });
    },
    sortProducts() {
      if (this.selectedSortOption === "name") {
        // Sort by brewery name
        this.products.sort((a, b) => a.name.localeCompare(b.name));
      } else if (this.selectedSortOption === "category") {
        // Sort by category
        this.products.sort((a, b) => a.category.localeCompare(b.category));
      } else if (this.selectedSortOption === "price") {
        // Sort by price
        this.products.sort((a, b) => a.price - b.price);
      }
    },
    filterProducts() {
      // Triggered when the category selection changes
      // Update filteredProducts based on selectedCategory
    },
  },
  computed: {
    uniqueCategories() {
      // Get unique categories from products
      const categories = new Set();
      this.products.forEach((product) => {
        categories.add(product.category);
      });
      return Array.from(categories);
    },
    filteredProducts() {
      let filtered = this.products;

      // Filter by category if selectedCategory is not empty
      if (this.selectedCategory !== "") {
        filtered = filtered.filter(
          (product) => product.category === this.selectedCategory
        );
      }

      // Sort filtered products based on selectedSortOption
      // Implement your sorting logic here

      return filtered;
    },
  },
  watch: {
    // Watch for changes in selectedSortOption
    selectedSortOption: {
      handler: "sortProducts", // Call sortProducts method
      immediate: true, // Sort initially when component is mounted
    },
  },
};
</script>

<style scoped>
.product-list {
  padding: 20px;
}

.filters {
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-right: 10px;
}

select {
  padding: 8px 12px;
  border: 1px solid #ccc;
  background-color: #f9f9f9;
  cursor: pointer;
}

.product-items {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}

.product-item {
  border: 1px solid #ccc;
  padding: 10px;
  background-color: #f9f9f9;
}
</style>
