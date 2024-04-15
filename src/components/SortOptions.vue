<template>
  <div class="sort-options">
    <button
      v-for="(option, index) in sortOptions"
      :key="index"
      @click="selectSortOption(option)"
    >
      {{ option.label }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sortOptions: [
        { label: "Brauerei", value: "name" },
        { label: "Sorte", value: "category" },
        { label: "Preis", value: "price" },
      ],
    };
  },
  methods: {
    selectSortOption(option) {
      console.log("Sort option selected:", option);
      this.$emit("sort", option.value);
    },
  },
};
</script>

<style scoped>
.sort-options {
  display: flex;
  justify-content: center;
  align-items: center;
}

button {
  margin: 0 5px;
  padding: 8px 12px;
  border: 1px solid #ccc;
  background-color: #f9f9f9;
  cursor: pointer;
}

button:hover {
  background-color: #eaeaea;
}

button:focus {
  outline: none;
}
</style>
