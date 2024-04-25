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
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value})
  newItem.value = ''
}
</script>

<template>
  <h1>{{ header }}</h1>
  <form
    class="add-item-form"
    @submit.prevent="saveItem"
  >
    <input
      v-model.trim="newItem" type="text" placeholder="Add an item"
    >
    Priority:
    <label>
      <input type="checkbox" v-model="newItemHighPriority">
      High Priority
    </label>
    <button
      class="btn btn-primary">
      Save Item
    </button>
  </form>
  <ul>
    <!-- Uncomment this line code if you care for nondestructure form -->
    <!-- <li v-for="item in items" :key="item.id">{{ item.label }}</li> -->
    <!-- Below, it is using destructure form -->
    <li v-for="{ id, label } in items" :key="id">{{ label }}</li>
  </ul>
</template>

