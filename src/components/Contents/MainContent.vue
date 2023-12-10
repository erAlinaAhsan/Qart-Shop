<template>
  <div>
    <div class="container mx-auto p-4">
      <div class="list-container" v-if="showListContainer">
        <div
          class="flex items-start mt-4"
          v-for="coffee in displayedCoffees"
          :key="coffee.id"
          display="flex"
          @click="toggleDetails(coffee)"
        >
          <img :src="coffee.image" class="imgs" />
          <p>
            <b>{{ coffee.title }}</b>
            <br />
          </p>
          <p class="description" v-show="coffee.showDetails">
            {{ coffee.description }}
          </p>
          <p v-show="coffee.showDetails">{{ coffee.ingredients }}</p>
          <p v-show="coffee.showDetails">{{ coffee.id }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainContent",
  props: {
    coffees: Array,
    imagePath9: String,
    showListContainer: Boolean,
    filteredCoffees: Array,
  },
  methods: {
    toggleDetails(coffee) {
      coffee.showDetails = !coffee.showDetails;
    },
  },
  computed: {
    displayedCoffees() {
      return this.showListContainer ? this.filteredCoffees : this.coffees;
    },
  },
};
</script>



<style scoped>
</style>
