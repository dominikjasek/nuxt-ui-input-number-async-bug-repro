<script setup lang="ts">

import { ref , watch} from 'vue'

const query = ref('')
const options = ref<{name:string}[]>([])

const serverData = [
  { name: 'Apple' },
  { name: 'Banana' },
  { name: 'Orange' },
  { name: 'Honeydew' },
  { name: 'Grapes' },
  { name: 'Watermelon' },
  { name: 'Cantaloupe' },
]

// Simulate an ajax search that populates combobox options from a server
watch(query, () => {
  options.value = []
  setTimeout(() => {
    if (query.value == '') {
      options.value = []
    }
    else {
      options.value = serverData.filter(item =>
        item.name.toLowerCase().includes(query.value.toLowerCase()),
      )
    }
  }, 500)
})

</script>


<template>
  <div v-for="option in options" :key="option.name">{{ option.name }}</div>
  <UInputMenu
    v-model:search-term="query"
    :items="options"
    ignore-filter
    placeholder="Select user"
  >
    <template #item="{ item }">
      <div>{{ item.name }}</div>
    </template>
  </UInputMenu>
</template>

