<template>
  <div>
    <nav class="flex items-center justify-between h-2 bg-black text-white p-4">
      <img :src="imagePath" class="menu-icon h-10 mb-12 border-radius-5" />
      <div
        class="search-box flex items-center mx-auto mb-12 border rounded-full p-2 bg-black"
      >
        <input
          type="text"
          v-model="searchQuery"
          placeholder="Search by ingredients..."
          @input="handleSearchInput"
          class="bg-transparent text-white focus:outline-none w-full"
        />
        <img :src="imagePath1" class="search-icon w-5 h-5 ml-2" />
      </div>
    </nav>

    <div
      class="flex-div1 flex items-center justify-evenly p-8 bg-black text-white"
    >
      <h4
        @click="emitAllButtonClick"
        :class="{ active: selectedIngredient === '' }"
        class="btn bg-gray-700 mr-5"
      >
        All
      </h4>

      <h4
        v-for="(ingredient, index) in ingredientsList"
        :key="index"
        @click="filterByIngredient(ingredient)"
        :class="{ active: selectedIngredient === ingredient }"
        class="tags bg-gray-700 border-rounded mr-5"
      >
        {{ ingredient }}
      </h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  props: {
    imagePath: String,
    imagePath1: String,
    ingredientsList: Array,
  },
  data() {
    return {
      searchQuery: "",
      selectedIngredient: "",
    };
  },
  created() {
    // Set "All" button as active by default
    this.selectedIngredient = "";
  },

  methods: {
    emitAllButtonClick() {
      console.log("Emitting allButtonClick event");
      this.selectedIngredient = "";
      this.$emit("allButtonClick");
    },
    filterByIngredient(ingredient) {
      this.selectedIngredient = ingredient;
      this.$emit("filterByIngredient", ingredient);
    },
    handleSearchInput() {
      // Emit the search query for handling in the parent component
      this.$emit("searchByIngredient", this.searchQuery);
    },
  },
};
</script>

<style scoped>
</style>
