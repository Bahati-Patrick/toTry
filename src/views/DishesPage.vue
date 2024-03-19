<script setup lang="ts">
import  { ref } from 'vue';
import type { Dish } from '@/types';
import { restaurantStatusList } from '@/constants';

const dishList = ref<Dish[]>([]);
const newDish = ref<Dish>({
  status: 'Want to Try'
});

function addDish () {
  dishList.value.push({
    name: newDish.value.name,
    status: newDish.value.status,
  });
}
</script>

<template>
  <main>
    <pre>
      {{ newDish }}
    </pre>
    <!-- form that will allow users to add a restaurant to a list -->
    <form @submit.prevent="addDish">
      <div>
        <label for="dish-name">Dish Name</label>
        <input id="dish-name" type="text" v-model="newDish.name">
      </div>

      <div>
        <label for="dish-status">Dish Status</label>
        <select 
          name="dish-status" 
          id="dish-status"
          v-model="newDish.status"
        >
          <option 
            v-for="status in restaurantStatusList"
            :value="status"
            :key="status"
          >
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Dish</button>
    </form>
    <ul>
      <li v-for="dish in dishList" :key="dish.name">
        {{ dish.name }} - {{ dish.status }}
      </li>
    </ul>
  </main>
</template>
