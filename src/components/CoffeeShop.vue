<template>
  <div class="bg-gray-100 text-gray-800">
    <NavBar
      :imagePath="imagePath"
      :imagePath1="imagePath1"
      @allButtonClick="toggleListContainer"
      @filterByIngredient="filterByIngredient"
      @searchByIngredient="handleSearchByIngredient"
      :ingredientsList="ingredientsList"
    />
    <SideBar />
    <MainContent
      :coffees="coffees"
      :imagePath9="imagePath9"
      :showListContainer="showListContainer"
      :filteredCoffees="filteredCoffees"
    />
  </div>
</template>

<script>
import NavBar from "@/components/Contents/NavBar.vue";
import SideBar from "@/components/Contents/SideBar.vue";
import MainContent from "@/components/Contents/MainContent.vue";

export default {
  name: "CoffeeShop",
  components: {
    NavBar,
    SideBar,
    MainContent,
  },
  data() {
    return {
      imagePath: require("@/assets/bar.png"),
      imagePath1: require("@/assets/search-icon.png"),
      coffees: [],
      showListContainer: false,
      filteredCoffees: [],
      ingredientsList: [],
      searchQuery: "",
    };
  },
  methods: {
    toggleListContainer() {
      if (!this.showListContainer) {
        this.filteredCoffees = [...this.coffees];
      }
      this.showListContainer = !this.showListContainer;
    },
    filterCoffees(filterFunction) {
      if (filterFunction) {
        this.filteredCoffees = this.coffees.filter(filterFunction);
      } else {
        this.filteredCoffees = [...this.coffees];
      }
      this.showListContainer = this.filteredCoffees.length > 0;
    },

    async fetchData() {
      try {
        const response = await fetch("https://api.sampleapis.com/coffee/hot");
        const data = await response.json();
        this.coffees = data.map((coffee) => ({
          ...coffee,
          showDetails: false,
        }));
        this.ingredientsList = this.extractUniqueIngredients();
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },

    extractUniqueIngredients() {
      console.log("coffees", this.coffees);
      let ingredientsArray = this.coffees.map((coffee) => {
        return coffee.ingredients;
      });
      const flatArray = ingredientsArray.flat();
      let ingredients = [...new Set(flatArray)];
      return ingredients;
    },

    filterByIngredient(ingredient) {
      const lowerCaseIngredient = ingredient.toLowerCase();
      this.filterCoffees((coffee) =>
        coffee.ingredients.some((coffeeIngredient) =>
          coffeeIngredient.toLowerCase().includes(lowerCaseIngredient)
        )
      );
    },
    handleSearchByIngredient(query) {
      this.searchQuery = query;
      this.filterCoffees((coffee) =>
        coffee.ingredients.some((coffeeIngredient) =>
          coffeeIngredient
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase())
        )
      );
    },
  },
  created() {
    this.fetchData()
      .then(() => {
        this.selectedIngredient = "";
        this.filterCoffees();
      })
      .catch((error) => {
        console.error("Error fetching data:", error);
      });
  },
  mounted() {
    var menuIcon = document.querySelector(".menu-icon");
    var sidebar = document.querySelector(".sidebar");
    var container = document.querySelector(".container");

    var imgsList = document.querySelectorAll(".imgs");
    var listcontainer = document.querySelector(".list-container");

    menuIcon.onclick = function () {
      sidebar.classList.toggle("small-sidebar");
      container.classList.toggle("large-container");
    };

    imgsList.forEach((img) => {
      img.onclick = function () {
        listcontainer.classList.toggle("listdesp-container");
      };
    });
  },
};
</script>


<style scoped>
* {
  margin: 0;
  padding: 0;
  font-family: "poppins", sans-serif;
  box-sizing: border-box;
}
</style>
