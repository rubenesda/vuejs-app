<script setup lang="ts">
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, label: '10 party hats' },
  { id: 2, label: '2 board games' },
  { id: 3, label: '20 cups' }
])
const newItem = ref('')
const newItemHighPriority = ref(false)
</script>

<template>
  <h1>{{ header }}</h1>
  <div class="add-item-form">
    <input
      v-model.trim="newItem" type="text" placeholder="Add an item"
      v-on:keyup.enter="items.push({ id: items.length + 1, label: newItem})"
    >
    Priority:
    <label>
      <input type="checkbox" v-model="newItemHighPriority">
      High Priority
    </label>
    <button
      v-on:click="items.push({ id: items.length + 1, label: newItem })"
      class="btn btn-primary">
      Save Item
    </button>
  </div>
  <ul>
    <!-- Uncomment this line code if you care for nondestructure form -->
    <!-- <li v-for="item in items" :key="item.id">{{ item.label }}</li> -->
    <!-- Below, it is using destructure form -->
    <li v-for="{ id, label } in items" :key="id">{{ label }}</li>
  </ul>
</template>

