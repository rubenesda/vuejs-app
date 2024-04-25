<script setup lang="ts">
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref({
  'item-1': { id: '1', label: '10 party hats' },
  'item-2': { id: '1', label: '2 board games' },
  'item-3': { id: '1', label: '20 cups' }
})
</script>

<template>
  <h1>{{ header }}</h1>
  <ul>
    <!-- Uncomment this line code if you care for nondestructure form -->
    <!-- <li v-for="item in items" :key="item.id">{{ item.label }}</li> -->
    <!-- Below, it is using destructure form -->
    <!-- Now. index variable are rendering the prepend 'item-#' for every object key from our object variable -->
    <li v-for="({ id, label }, index) in items" :key="id">
      {{ index }}
      {{ label }}
    </li>
  </ul>
</template>

