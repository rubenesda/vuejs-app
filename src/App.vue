<script setup lang="ts">
import { ref, type Ref } from 'vue'

const header = ref('Shopping List App')
const editing = ref(false)
const items: Ref<Array<{ id: number, label: string}>> = ref([])
const newItem = ref('')
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value})
  newItem.value = ''
}
const doEdit = (e: boolean) => {
  editing.value = e
  newItem.value = ''
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
  <a v-bind:href="newItem">Dynamic Link</a>
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
  <p v-if="!items.length">
    Nothing to see here
  </p>
</template>

