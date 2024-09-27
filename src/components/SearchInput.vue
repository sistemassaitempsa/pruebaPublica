<template>
  <div class="search-container">
    <input
      v-model="searchValue"
      type="number"
      placeholder="Buscar cédula"
      class="search-input"
    />
    <button @click="search" type="button" class="search-button">
      <i class="fas fa-search"></i>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchValue: null,
    };
  },
  methods: {
    search() {
      console.log("Buscando por:", this.searchValue);
      this.$emit("search", this.searchValue);
    },
  },
};
</script>

<style scoped>
.search-container {
  display: flex;
  align-items: center;
}

.search-input {
  flex: 1;
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px 0 0 4px;
}

.search-button {
  padding: 0.5rem;
  border: none;
  background-color: #006b3f;
  color: white;
  cursor: pointer;
  border-radius: 0 4px 4px 0;
}

.search-button i {
  font-size: 1rem;
}

.search-button:hover {
  background-color: #015734;
}
</style>
