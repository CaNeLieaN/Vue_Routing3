<template>
  <main class="container">
    <h1>Our Cars</h1>
    <select @change="handleChange" v-model="make">
      <option disabled value="">Please select one</option>
      <option value="All">All</option>
      <option value="Audi">Audi</option>
      <option value="Buick">Buick</option>
      <option value="Chevrolet">Chevrolet</option>
      <option value="Porsche">Porsche</option>
    </select>
    <div class="cards">
      <RouterLink
        :to="`car/${car.id}`"
        v-for="car in cars"
        :key="car.id"
        class="card"
      >
        <h1>{{ car.make }}</h1>
        <p>${{ car.price }}</p>
      </RouterLink>
    </div>
  </main>
</template>
  
<script setup>
import carsData from "../data.json";
import { onMounted, ref, watch } from "vue";
import { RouterLink } from "vue-router";
import { useRouter, useRoute } from "vue-router";

const router = useRouter();
const route = useRoute();

const cars = ref(carsData);
const make = ref("");

onMounted(() => {
  make.value = route.query.make;
});

watch(make, () => {
  if (make.value) {
    if (make.value === "All") cars.value = carsData;
    else {
      cars.value = carsData.filter((c) => c.make === make.value);
    }
  }
});

const handleChange = () => {
  router.push({ query: { make: make.value } });
};
</script>
  
<style scoped>
.cards {
  display: flex;
  width: 1000px;
  flex-wrap: wrap;
  margin-top: 50px;
  justify-content: center;
}

.card {
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.207);
  padding: 15px;
  width: 150px;
  margin-right: 15px;
  cursor: pointer;
  margin-bottom: 20px;
}
</style>
