<script setup lang="js">
  import AddItems from './components/AddItems.vue'
  import SearchItems from './components/SearchItems.vue'
  import { provide, ref } from 'vue'

  const listItems = ref(['default item', 'another item'])

  const addItem = (e) => {
    console.log(e)
    listItems.value.push(e)
  }
  provide('addItemInAncestor', addItem)
</script>

<template>
  <div style="display: flex; flex-direction: column; gap: 25px">
    <ul v-for="(item, index) in listItems" :key="index">
      {{
        item
      }}
    </ul>
  </div>

  <AddItems @add-item="($event) => addItem($event)" />
  <SearchItems :listItems="listItems" />
</template>

<style scoped></style>
