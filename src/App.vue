<script setup lang="ts">
import { ref, type Ref, computed } from 'vue'

const header = ref('Shopping List App')
const reversedItems = computed(() => [...items.value].reverse())
const editing = ref(false)
const items: Ref<Array<{ id: number, label: string, purchased: boolean, highPriority: boolean}>> = ref([
  // Previous data
  {
    id: 1,
    label: "10 party hats",
    purchased: true,
    highPriority: false,
  },
  {
    id: 2,
    label:"2 board games",
    purchased: true,
    highPriority: false,
  },
  {
    id: 3,
    label: "20 cups",
    purchased: false,
    highPriority: true,
  }
])
const newItem = ref('')
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    purchased: false,
    highPriority: newItemHighPriority.value,
  })
  newItem.value = ''
  newItemHighPriority.value = false
}
const doEdit = (e: boolean) => {
  editing.value = e
  newItem.value = ''
  newItemHighPriority.value = false
}
const togglePurchased = (item: {id: number, label: string, purchased: boolean, highPriority: boolean }) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">
      Cancel
    </button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">
      Add item
    </button>
  </div>
  <form
    class="add-item-form"
    v-if="editing"
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
      :disabled="newItem.length < 5"
      class="btn btn-primary">
      Save Item
    </button>
  </form>
  <ul>
    <!-- Uncomment this line code if you care for nondestructure form -->
    <!-- <li v-for="item in items" :key="item.id">{{ item.label }}</li> -->
    <!-- Below, it is using destructure form -->
    <li v-for="{ id, label, purchased, highPriority}, index in reversedItems"
      @click="togglePurchased(reversedItems[index])"
      :key="id"
      class="static-class"
      :class="{
        strikeout: purchased,
        priority: highPriority
      }"
    >
      {{ label }}
    </li>
  </ul>
  <p v-if="!items.length">
    Nothing to see here
  </p>
</template>

