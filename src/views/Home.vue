<template>
  <div class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-bold mb-4">Random Meals</h1>
  </div>
  <Meals :meals="meals" />
</template>

<script>
import { onMounted, ref } from "vue";
import axiosClient from "../axiosClient.js";
import Meals from "../components/Meals.vue";

export default {
  name: "Home",
  components: { Meals },
  setup() {
    const meals = ref([]);

    onMounted(async () => {
      for (let i = 0; i < 10; i++) {
        axiosClient
          .get(`random.php`)
          .then(({ data }) => meals.value.push(data.meals[0]));
      }
    });

    return {
      meals,
    };
  },
};
</script>

<style scoped></style>
