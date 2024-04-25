<script setup lang="ts">
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: '1', label: '10 party hats' },
  { id: '1', label: '2 board games' },
  { id: '1', label: '20 cups' }
])
const newItem = ref('')
const newItemPriority = ref('low')
</script>

<template>
  <h1>{{ header }}</h1>
  <input v-model.trim="newItem" type="text" placeholder="Add an item">
  {{ newItem }}
  <!-- v-model will work with select input -->
  Priority:
  <select v-model="newItemPriority">
    <option value="low">Low</option>
    <option value="high">High</option>
  </select>
  <br/>
  {{ newItemPriority }}
  <ul>
    <!-- Uncomment this line code if you care for nondestructure form -->
    <!-- <li v-for="item in items" :key="item.id">{{ item.label }}</li> -->
    <!-- Below, it is using destructure form -->
    <li v-for="{ id, label } in items" :key="id">{{ label }}</li>
  </ul>
</template>

